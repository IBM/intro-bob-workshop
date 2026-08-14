# Examples — Agent with Bob Shell

How to invoke this skill and what it produces.

---

## Example 1: CLI Report Analysis Agent

**You say:**
> "Create an agentic Python app that reads two monthly business reports and writes a follow-up brief. Use Bob Shell for all LLM work."

**What the skill builds:**

```
my-agent/
├── agent.py              ← orchestrator: bob() helper + Plan→Act→Eval loop
├── reports/
│   ├── january.md        ← input A
│   └── february.md       ← input B
└── follow-up-brief.md    ← written by Bob during the Act phase
```

**How to run it:**
```bash
export BOB_API_KEY="..."
python3 agent.py
python3 agent.py --report-a q1.md --report-b q2.md --output q2-brief.md
```

**What happens on each iteration:**

| Phase | Bob mode | Bob does |
|-------|----------|----------|
| Plan | `--mode ask` | Describes the next action in plain text — no file access |
| Act | *(default)* | Reads both reports, compares metrics, writes the brief |
| Eval | `--mode ask` | Checks the brief for required sections, returns `{"done": true/false, ...}` |

The loop stops when Eval returns `"done": true`, or when `--max-iterations` is reached.

---

## Example 2: Web UI with Real-Time Progress

**You say:**
> "Build the same agent but with a web UI — drag-and-drop upload, live progress feed, rendered output."

**What the skill builds:**

```
my-agent/
├── agent.py              ← same orchestrator, reused by the server
└── app/
    ├── server.py         ← Flask server: POST /api/analyze, GET /api/stream/<job_id>
    ├── index.html        ← SPA: drag-drop upload, SSE progress panels, brief renderer
    └── requirements.txt  ← flask>=3.0, markdown>=3.6
```

**What the user sees in the browser:**

1. Two drag-and-drop zones — drop the Markdown report files
2. Click **Run Analysis** — the loop starts immediately
3. Each Plan / Act / Evaluate phase appears as it completes (Server-Sent Events)
4. The Act phase shows a tool trace table — what Bob read and wrote
5. When done, the formatted brief renders inline with Copy / Download buttons

---

## Application architecture

```
┌─────────────────────────────────────────────────────────┐
│                   Your Python Code                       │
│                   (orchestrator)                         │
│                                                         │
│   goal ──► for each iteration:                          │
│                │                                        │
│           ┌────▼────┐   mode=ask        ┌───────────┐  │
│           │  PLAN   │──────────────────►│ bob run   │  │
│           │         │◄── plain text ────│ --mode ask│  │
│           └────┬────┘                   └───────────┘  │
│                │ plan                                   │
│           ┌────▼────┐   default agent   ┌───────────┐  │
│           │   ACT   │──────────────────►│ bob run   │  │
│           │         │◄── tool trace     │ (+ tools) │  │
│           │         │    + summary ─────└───────────┘  │
│           └────┬────┘                                   │
│                │ action_result                          │
│           ┌────▼────┐   mode=ask        ┌───────────┐  │
│           │  EVAL   │──────────────────►│ bob run   │  │
│           │         │◄── {"done":...} ──│ --mode ask│  │
│           └────┬────┘                   └───────────┘  │
│                │                                        │
│         done? ─┴─ no → update state → next iteration   │
└─────────────────────────────────────────────────────────┘
```

**Roles:**
- Your Python code — owns the loop, state, file scaffolding, and the goal definition
- `bob run --mode ask` — reasons without touching files (Plan, Eval)
- `bob run` (default) — reads inputs, writes outputs using file tools (Act)
- `BOB_API_KEY` — the only credential needed; no LLM SDK or API client required

---

## Reference files

| File | What's inside |
|------|---------------|
| [references/CODE.md](references/CODE.md) | `bob()` helper, `bob_act()` stream-json parser, `run_loop()`, Flask+SSE server, SSE JS client, CLI entry point |
| [references/PROMPT_TEMPLATES.md](references/PROMPT_TEMPLATES.md) | `PLAN_PROMPT`, `ACT_PROMPT`, `EVAL_PROMPT` with placeholder docs and adaptation guide |
| [references/REFERENCE.md](references/REFERENCE.md) | `bob run` flags, output schemas, workspace isolation, auth, gotchas |
