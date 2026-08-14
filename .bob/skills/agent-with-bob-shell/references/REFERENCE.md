# Reference — Agent with Bob Shell

Detailed technical reference for embedding IBM Bob Shell in an agentic loop. Read this when you need the exact schemas, gotchas, or advanced options.

---

## Authentication

`bob run` requires a `BOB_API_KEY` environment variable. Interactive `bob chat` can use browser SSO, but non-interactive `bob run` does not.

**Get a key:** Bob web portal → Account → API Keys → New key → **Scope: Inference** → copy immediately.

```bash
# Temporary (this session only)
export BOB_API_KEY="bob_..."

# Permanent
echo 'export BOB_API_KEY="bob_..."' >> ~/.zshrc && source ~/.zshrc
```

**Verify:**
```bash
bob run "Say hello in one sentence." --log-level silent
```

> **Note — General-scope keys:** If your key has **General** scope instead of Inference, add `--team-id <id>` to every `bob run` call. Inference-scoped keys are simpler — prefer them.

---

## `bob run` CLI Reference

```
bob run "<prompt>" [flags]
```

| Flag | Effect |
|------|--------|
| `--format json` | Single JSON object on stdout when session ends. Contains `last_message`, `stats`. |
| `--format stream-json` | NDJSON stream — one JSON event per line as Bob works. Includes tool calls. |
| `--log-level silent` | Suppress all progress/trace output. Only the result reaches stdout. |
| `--mode <slug>` | Shift reasoning posture. `ask` = no tools. `plan` = strategic. *(omit)* = full agent. |
| `-w <dir>` | Set Bob's workspace. Bob can only read/write files inside `<dir>`. |
| `--max-turns <n>` | Cap the number of model turns per invocation. |
| `--max-cost <n>` | Cap spend (USD) per invocation. |

### `--format json` output schema

```json
{
  "type": "result",
  "status": "success",
  "last_message": "The full final assistant response as a single string.",
  "stats": {
    "total_tokens": 1840,
    "session_costs": 0.003,
    "tool_calls": 4
  }
}
```

Extract the answer: `data.get("last_message", raw_stdout).strip()`

### `--format stream-json` event schema

One JSON object per line (NDJSON). Events arrive in this order:

```jsonc
// 1. Prompt echo
{"type": "message", "role": "user", "content": "...the prompt..."}

// 2. Tool call (one per tool Bob invokes)
{"type": "tool_use",    "tool_id": "abc123", "tool_name": "read_file",  "parameters": {"path": "report_a.md"}}
{"type": "tool_result", "tool_id": "abc123", "status": "success",       "output": "# January Report\n..."}

// 3. Assistant response — streamed one token per line
{"type": "message", "role": "assistant", "content": "I have read"}
{"type": "message", "role": "assistant", "content": " both reports"}
{"type": "message", "role": "assistant", "content": " and compared..."}

// 4. Terminal event — NO last_message field in this version
{"type": "result", "status": "success", "stats": {"total_tokens": 2100, "tool_calls": 3}}
```

**Critical:** The `result` event does **not** contain `last_message` in stream-json mode. You must reconstruct the assistant's prose by concatenating all `{"type":"message","role":"assistant","content":"<token>"}` events.

**Tool correlation:** `tool_use` and `tool_result` are matched by `tool_id` (not position). Always key by `tool_id`.

---

## Workspace isolation (`-w`)

Bob's file tools (`read_file`, `write_file`, `list_files`, etc.) are **sandboxed** to the directory passed to `-w`. If you pass `-w /tmp/job_42/`, Bob can only see files inside that directory.

**Pattern for CLI scripts:**
```python
"-w", str(Path(__file__).parent)   # workspace = the script's own directory
```

**Pattern for web servers (per-job isolation):**
```python
job_dir = Path(tempfile.mkdtemp()) / job_id
job_dir.mkdir()
# copy/save uploaded files into job_dir
"-w", str(job_dir)                  # each job is isolated
```

**File references in prompts:**  
Because the workspace IS `job_dir`, refer to files by plain name — `report_a.md`, not `/tmp/job_42/report_a.md`.

---

## Mode selection by phase

| Phase | Mode | Why |
|-------|------|-----|
| **Plan** | `--mode ask` | No tool access — Bob describes the next action but cannot accidentally execute it. |
| **Act** | *(default)* | Full tool access — Bob reads inputs, writes outputs, uses any available tool. |
| **Evaluate** | `--mode ask` | No tool access — Bob reasons about whether the output meets criteria. |

Using `ask` for Plan and Eval is a **safety constraint**: it makes the phases deterministic and prevents Bob from skipping steps or doing the wrong work in the wrong phase.

---

## State management

`bob run` is **stateless** — each call starts a fresh session with no memory of previous calls. Your Python code is the sole memory:

- `goal` — the original task description (never changes)
- `state` — what still needs to be done (updated by Eval's `next_state` each iteration)
- Inject both into every Plan prompt via `PLAN_PROMPT.format(goal=goal, state=state)`

---

## Eval JSON contract

The Evaluator phase must return a specific JSON shape. Enforce it in the prompt:

```
Reply ONLY with valid JSON — no markdown fences, no extra text:
{
  "done": true or false,
  "reason": "one sentence explanation",
  "next_state": "if done is false, describe precisely what is still missing"
}
```

Parse with `json.loads()`. If parsing fails (Bob added markdown fences or extra prose), catch `JSONDecodeError` and re-plan with `state = "Evaluator returned invalid JSON — re-read the output and fix issues."`.

---

## Common gotchas

| Symptom | Cause | Fix |
|---------|-------|-----|
| `Error: Bob API key is required` | `BOB_API_KEY` not set | `export BOB_API_KEY="..."` |
| Bob says "I can't read that file" | File is outside the `-w` workspace | Copy file into the workspace dir |
| `last_message` is empty/missing | Using `--format stream-json` and reading `result` event | Concatenate `role:assistant` message tokens instead |
| Eval never returns `done: true` | Model wraps JSON in ```json fences | Strip fences before `json.loads()`, or add fence-stripping to the prompt |
| Tool names show as "unknown" | Pairing `tool_result` by position instead of `tool_id` | Always correlate by `tool_id` field |
| Act phase writes to wrong path | Prompt uses absolute path; workspace is relative | Use plain filename in prompt, pass `-w <dir>` |
| `pip3` / `python3` mismatch | Different interpreters | Use `python3 -m pip install` not bare `pip3` |

---

## Cost and turn controls

Add these to any `bob run` call to prevent runaway spending:

```python
cmd += ["--max-turns", "20"]    # max model turns per invocation
cmd += ["--max-cost",  "0.10"]  # max USD per invocation
```

For the Act phase (most expensive), a limit of `--max-turns 20` and `--max-cost 0.20` is a reasonable starting point.
