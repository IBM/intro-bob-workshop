# Code Reference — Agent with Bob Shell

Complete, copy-paste code patterns. Each section is self-contained.

Prompt templates (PLAN_PROMPT, ACT_PROMPT, EVAL_PROMPT) → [PROMPT_TEMPLATES.md](PROMPT_TEMPLATES.md)

---

## bob() helper

The only function that knows about Bob Shell. Used for **Plan** and **Evaluate** phases.

```python
import json
import subprocess
import sys
from pathlib import Path

def bob(prompt: str, workspace: Path, mode: str | None = None) -> str:
    """
    Call Bob Shell non-interactively. Returns the final assistant text.

    Uses --format json       →  result has {"last_message": "..."}
    Uses --log-level silent  →  only the result reaches stdout
    Uses -w <workspace>      →  Bob can only read/write inside that directory
    """
    cmd = [
        "bob", "run",
        prompt,
        "--format", "json",
        "--log-level", "silent",
        "-w", str(workspace),
    ]
    if mode:
        cmd += ["--mode", mode]

    result = subprocess.run(cmd, capture_output=True, text=True)

    if result.returncode != 0:
        print(f"[ERROR] bob run exited {result.returncode}", file=sys.stderr)
        print(result.stderr, file=sys.stderr)
        sys.exit(result.returncode)

    try:
        data = json.loads(result.stdout)
        return data.get("last_message", result.stdout).strip()
    except json.JSONDecodeError:
        return result.stdout.strip()
```

---

## bob_act() helper

Used for the **Act** phase only. Returns a tool trace (what Bob read/wrote) **and** the assistant prose summary. Uses `--format stream-json` so you can show the user exactly what tools Bob invoked.

```python
def bob_act(prompt: str, workspace: Path) -> tuple[list[dict], str]:
    """
    Call Bob Shell with --format stream-json for the Act phase.

    Returns:
        tools   — list of {"tool", "input", "output", "status"}, one per tool call
        summary — assistant prose (concatenated from streamed message tokens)

    stream-json schema (NDJSON, one event per line):
      {"type":"message",    "role":"user",      "content":"..."}      prompt echo
      {"type":"tool_use",   "tool_id":"x",      "tool_name":"...",    "parameters":{...}}
      {"type":"tool_result","tool_id":"x",      "status":"success",   "output":"..."}
      {"type":"message",    "role":"assistant",  "content":"<token>"}  one token per line
      {"type":"result",     "status":"success",  "stats":{...}}        NO last_message here
    """
    cmd = [
        "bob", "run",
        prompt,
        "--format", "stream-json",
        "--log-level", "silent",
        "-w", str(workspace),
    ]
    result = subprocess.run(cmd, capture_output=True, text=True)

    if result.returncode != 0:
        raise RuntimeError(result.stderr.strip() or f"bob run exited {result.returncode}")

    # Correlate tool_use ↔ tool_result by tool_id (NOT by position)
    by_id: dict[str, dict] = {}
    order: list[str] = []
    tokens: list[str] = []

    for raw in result.stdout.splitlines():
        raw = raw.strip()
        if not raw:
            continue
        try:
            event = json.loads(raw)
        except json.JSONDecodeError:
            continue

        etype   = event.get("type", "")
        tool_id = event.get("tool_id", "")

        if etype == "tool_use":
            params = event.get("parameters", {})
            input_str = ", ".join(
                f"{k}={repr(v)[:120]}" for k, v in params.items()
            ) if isinstance(params, dict) else str(params)[:240]
            by_id[tool_id] = {
                "tool":   event.get("tool_name", "unknown"),
                "input":  input_str,
                "output": "",
                "status": "",
            }
            order.append(tool_id)

        elif etype == "tool_result":
            entry = by_id.get(tool_id)
            if entry is None:                           # orphaned result
                entry = {"tool": "unknown", "input": "", "output": "", "status": ""}
                by_id[tool_id] = entry
                order.append(tool_id)
            output = event.get("output", "")
            if isinstance(output, str) and len(output) > 400:
                output = output[:400] + f"\n… ({len(output) - 400} chars truncated)"
            entry["output"] = output
            entry["status"] = event.get("status", "")

        elif etype == "message" and event.get("role") == "assistant":
            content = event.get("content", "")
            if isinstance(content, str):
                tokens.append(content)

        # "result" event intentionally ignored — it has no last_message in stream-json

    tools   = [by_id[tid] for tid in order if tid in by_id]
    summary = "".join(tokens).strip()
    return tools, summary
```

---

## Agentic loop

Assumes `bob()`, `bob_act()`, and the three prompt templates are already imported/defined.

```python
from pathlib import Path

def run_loop(
    input_a: str,
    input_b: str,
    output: str,
    workspace: Path,
    max_iterations: int = 4,
) -> None:
    goal = (
        f"Read @{input_a} and @{input_b}. "
        "Compare the two months across all key business metrics. "
        f"Write {output} containing: "
        "(1) an executive summary, "
        "(2) a month-over-month metric comparison table, "
        "(3) at least three prioritised action items with an owner role for each."
    )
    state = goal   # state evolves each iteration; goal never changes

    for i in range(max_iterations):
        print(f"\n{'━' * 60}  Iteration {i+1}/{max_iterations}  {'━' * 60}\n")

        # ── PLAN ──────────────────────────────────────────────────
        # ask mode = no tools, can only describe the next action
        plan = bob(
            PLAN_PROMPT.format(goal=goal, state=state),
            workspace=workspace,
            mode="ask",
        )
        print(f"[PLAN]\n{plan}\n")

        # ── ACT ───────────────────────────────────────────────────
        # default agent mode = full tool access (read_file, write_file, …)
        tools, action_result = bob_act(
            ACT_PROMPT.format(plan=plan, input_a=input_a, input_b=input_b, output=output),
            workspace=workspace,
        )
        print(f"[TOOLS]  {[t['tool'] for t in tools]}")
        print(f"[ACT]\n{action_result}\n")

        # ── EVAL ──────────────────────────────────────────────────
        # ask mode = no tools, pure reasoning
        eval_raw = bob(
            EVAL_PROMPT.format(goal=goal, action_result=action_result, output=output),
            workspace=workspace,
            mode="ask",
        )
        print(f"[EVAL RAW]\n{eval_raw}\n")

        try:
            result = json.loads(eval_raw)
        except json.JSONDecodeError:
            print("[WARN] Eval output was not valid JSON — re-planning.")
            state = "Evaluator returned invalid JSON. Re-read the output and fix any issues."
            continue

        status = "✓ done" if result["done"] else "✗ continuing"
        print(f"[EVAL] {status} — {result['reason']}")

        if result["done"]:
            print(f"\n✅  Goal achieved! Output written to {workspace / output}")
            return

        # Feed next_state back into Plan for the next iteration
        state = result.get("next_state", goal)

    print(f"\n⚠️  Reached max iterations ({max_iterations}) without completing.")
```

---

## Flask + SSE web UI wrapper

Wrap the loop for a browser UI: upload two files, watch phases stream in real time, read the rendered output.

### server.py skeleton

```python
import json, os, queue, shutil, subprocess, sys, tempfile, threading, uuid
from pathlib import Path
import markdown as md
from flask import Flask, Response, jsonify, request, send_from_directory

app = Flask(__name__, static_folder=".", static_url_path="")

_TMP_DIR = Path(tempfile.mkdtemp(prefix=f"agent_{os.getpid()}_"))
_jobs: dict[str, queue.Queue] = {}
_jobs_lock = threading.Lock()

import atexit; atexit.register(lambda: shutil.rmtree(_TMP_DIR, ignore_errors=True))

def _sse(event: str, data: dict) -> str:
    return f"event: {event}\ndata: {json.dumps(data)}\n\n"

def _run_loop_streaming(job_dir: Path, max_iter: int, q: queue.Queue) -> None:
    def emit(phase, iteration, text):
        q.put({"phase": phase, "iteration": iteration, "text": text})
    try:
        # ... call plan/act/eval using bob() and bob_act() wrappers ...
        # for the done event:
        brief_html = md.markdown(
            (job_dir / "output.md").read_text(),
            extensions=["tables", "fenced_code"],
        )
        q.put({"phase": "done", "iteration": i+1, "brief_html": brief_html})
    except Exception as exc:
        q.put({"phase": "error", "iteration": 0, "text": str(exc)})
    finally:
        q.put(None)                              # sentinel closes SSE stream
        shutil.rmtree(job_dir, ignore_errors=True)

@app.route("/api/analyze", methods=["POST"])
def analyze():
    job_id  = str(uuid.uuid4())
    job_dir = _TMP_DIR / job_id
    job_dir.mkdir()
    (job_dir / "input_a.md").write_bytes(request.files["file_a"].read())
    (job_dir / "input_b.md").write_bytes(request.files["file_b"].read())
    q: queue.Queue = queue.Queue()
    with _jobs_lock: _jobs[job_id] = q
    threading.Thread(
        target=_run_loop_streaming, args=(job_dir, 4, q), daemon=True
    ).start()
    return jsonify({"job_id": job_id})

@app.route("/api/stream/<job_id>")
def stream(job_id: str):
    with _jobs_lock: q = _jobs.get(job_id)
    if q is None: return jsonify({"error": "Not found"}), 404
    def generate():
        while True:
            item = q.get()
            if item is None:
                with _jobs_lock: _jobs.pop(job_id, None)
                yield _sse("close", {})
                return
            yield _sse(item.get("phase", "info"), item)
    return Response(generate(), mimetype="text/event-stream",
                    headers={"Cache-Control": "no-cache", "X-Accel-Buffering": "no"})

if __name__ == "__main__":
    port = int(os.environ.get("SERVER_PORT", 5001))
    print(f"http://localhost:{port}")
    app.run(host="0.0.0.0", port=port, threaded=True, debug=False)
```

### SSE client (JavaScript)

```javascript
const es = new EventSource(`/api/stream/${jobId}`);

es.addEventListener("plan",      e => renderPhase("plan", JSON.parse(e.data)));
es.addEventListener("act",       e => renderPhase("act",  JSON.parse(e.data)));
es.addEventListener("eval",      e => renderPhase("eval", JSON.parse(e.data)));
es.addEventListener("act_tools", e => renderToolTrace(JSON.parse(e.data).tools));
es.addEventListener("done",  e => { renderBrief(JSON.parse(e.data).brief_html); es.close(); });
es.addEventListener("error", e => { showError(JSON.parse(e.data).text);         es.close(); });
es.addEventListener("close", () => es.close());
```

### requirements.txt

```
flask>=3.0
markdown>=3.6
```

---

## Complete CLI entry point

```python
import argparse

_HERE = Path(__file__).parent

if __name__ == "__main__":
    p = argparse.ArgumentParser()
    p.add_argument("--input-a",        default=str(_HERE / "reports/january.md"))
    p.add_argument("--input-b",        default=str(_HERE / "reports/february.md"))
    p.add_argument("--output",         default="follow-up-brief.md")
    p.add_argument("--max-iterations", type=int, default=4)
    args = p.parse_args()

    for label, path in [("--input-a", args.input_a), ("--input-b", args.input_b)]:
        if not Path(path).exists():
            print(f"[ERROR] {label}: file not found: {path}", file=sys.stderr)
            sys.exit(1)

    run_loop(
        input_a=Path(args.input_a).name,    # plain name — workspace is _HERE
        input_b=Path(args.input_b).name,
        output=args.output,
        workspace=_HERE,
        max_iterations=args.max_iterations,
    )
```

> **Note:** ensure input files are inside the workspace directory, or adjust `-w` to the directory containing them.

