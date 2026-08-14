---
name: agent-with-bob-shell
description: Build a Python agentic loop application where IBM Bob Shell handles every LLM task (plan, act, evaluate). Covers the bob() subprocess helper, Plan→Act→Evaluate loop structure, prompt templates, workspace isolation with -w, mode selection per phase, stream-json tool-trace parsing, and a Flask+SSE web UI wrapper. Use when the user wants to create an agentic app, embed Bob Shell into a loop, build a plan/act/eval agent, or use bob run as an LLM backend.
---

# Agent with Bob Shell

Build a Python program that runs an agentic **Plan → Act → Evaluate** loop where every LLM call is made by spawning `bob run` as a subprocess.

## Architecture

```
Your Python code (orchestrator)
  │
  ├── PLAN   →  bob run "<plan_prompt>"  --mode ask     → plain text: "next action"
  ├── ACT    →  bob run "<act_prompt>"   --format stream-json   → writes files, returns tool trace + summary
  └── EVAL   →  bob run "<eval_prompt>"  --mode ask     → JSON: {"done":bool, "reason":"...", "next_state":"..."}
```

- Python owns state, loop control, and file I/O scaffolding  
- Bob Shell owns all reasoning and file operations inside its workspace  
- No LLM SDK, no API client — just `subprocess.run(["bob", "run", ...])`

## Quickstart checklist

- [ ] Confirm `bob` is on PATH: `bob --version`
- [ ] Set `BOB_API_KEY` env var (Inference scope — see [references/REFERENCE.md](references/REFERENCE.md#authentication))
- [ ] Verify: `bob run "Say hi." --log-level silent`
- [ ] Copy the `bob()` helper from [references/CODE.md](references/CODE.md#bob-helper)
- [ ] Copy the prompt templates from [references/PROMPT_TEMPLATES.md](references/PROMPT_TEMPLATES.md)
- [ ] Implement the loop from [references/CODE.md](references/CODE.md#agentic-loop)
- [ ] (Optional) Add Flask+SSE web UI — see [references/CODE.md](references/CODE.md#flask--sse-web-ui-wrapper)

## Key rules

| Rule | Why |
|------|-----|
| Always pass `-w <workspace_dir>` | Bob can only read/write inside that directory. Use `Path(__file__).parent` for CLI scripts; a per-job temp dir for web servers. |
| Use `--mode ask` for Plan & Eval | Prevents Bob from executing tools during reasoning-only phases. |
| Use `--format json` for Plan & Eval | Returns `{"last_message": "..."}` — easy to extract the answer. |
| Use `--format stream-json` for Act | Gives you a tool trace (what Bob read/wrote) and the assistant prose. |
| Pass `--log-level silent` always | Suppresses progress output — only the result reaches stdout. |
| File references in prompts use plain names | Because the workspace IS the directory you passed to `-w`. |
| Eval must return JSON | Instruct Bob explicitly: "Reply ONLY with valid JSON — no markdown fences". |
| Feed `next_state` back into Plan | This is how the loop self-corrects without external memory. |

## Mode reference

| Mode slug | What Bob does |
|-----------|---------------|
| *(omit)* | Default agent — can read files, write files, run tools |
| `ask` | Read-only reasoning — no tool access, safe for Plan & Eval |
| `plan` | Strategic reasoning — lighter tool access |

## Phase prompt shapes

**Plan** (mode=ask, format=json)
> "You are the planning phase… describe the single next action in 2-4 sentences. Do NOT execute it."

**Act** (default mode, format=stream-json)
> "Execute this plan exactly: {plan}. Files available: {files}. Write output to: {output}."

**Eval** (mode=ask, format=json)  
> "Evaluate whether the goal is achieved. Check that {output} contains ALL of: … Reply ONLY with valid JSON: {done, reason, next_state}"

Prompt templates → [references/PROMPT_TEMPLATES.md](references/PROMPT_TEMPLATES.md)
Full stream-json schema → [references/REFERENCE.md](references/REFERENCE.md#format-stream-json-event-schema)
