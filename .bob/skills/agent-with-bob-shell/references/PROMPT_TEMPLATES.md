# Prompt Templates — Agent with Bob Shell

Module-level string constants. Keep them here (not inline) so they are easy to tune independently of loop logic.

Each template uses Python `.format()` placeholders. Double-brace `{{` / `}}` escapes literal curly braces for the JSON example in `EVAL_PROMPT`.

---

## PLAN_PROMPT

Used in the **Plan** phase with `mode="ask"` — Bob may only describe the next action, not execute it.

```python
PLAN_PROMPT = """
You are the planning phase of an agentic loop. Your only job is to DESCRIBE
the next action — you must NOT read files, write files, or use any tools.

Overall goal:
{goal}

Current state:
{state}

In 2–4 plain sentences, describe the single most important next action.
Name specific files where relevant. Do not produce any output beyond this
description. Do not attempt to execute the action.
"""
```

**Placeholders:**

| Placeholder | Value |
|-------------|-------|
| `{goal}` | The original, never-changing task description |
| `{state}` | On iteration 1, same as `goal`. On subsequent iterations, the `next_state` string returned by the previous Eval. |

---

## ACT_PROMPT

Used in the **Act** phase with default agent mode — Bob has full tool access.

```python
ACT_PROMPT = """
You are the action phase of an agentic loop.

Execute the following plan exactly:
{plan}

Files available:
- {input_a}
- {input_b}

Write your output to: {output}

The output must contain:
1. Executive Summary  (3–5 sentences)
2. Month-over-Month Metric Comparison  (Markdown table)
3. Action Items  (numbered list, at least 3, each with an owner role)
"""
```

**Placeholders:**

| Placeholder | Value |
|-------------|-------|
| `{plan}` | The plain-text plan returned by the Plan phase |
| `{input_a}` | Plain filename of the first input (e.g. `report_a.md`) — no path prefix needed because `-w` sets the workspace |
| `{input_b}` | Plain filename of the second input |
| `{output}` | Plain filename of the output to write (e.g. `follow-up-brief.md`) |

> **Adapt this template** to your domain: replace the three required sections with whatever structure your output needs.

---

## EVAL_PROMPT

Used in the **Evaluate** phase with `mode="ask"` — Bob reasons about the output and returns a structured JSON verdict.

```python
EVAL_PROMPT = """
You are the evaluation phase of an agentic loop.

Overall goal:
{goal}

The agent just completed this action:
{action_result}

Evaluate whether the goal is fully achieved.
Check that {output} exists and contains ALL of:
  - An executive summary paragraph
  - A month-over-month metric comparison table
  - At least three numbered action items

Reply ONLY with valid JSON — no markdown fences, no extra text:
{{
  "done": true or false,
  "reason": "one sentence explanation",
  "next_state": "if done is false, describe precisely what is still missing or wrong"
}}
"""
```

**Placeholders:**

| Placeholder | Value |
|-------------|-------|
| `{goal}` | The original task description |
| `{action_result}` | The assistant prose summary returned by the Act phase |
| `{output}` | The output filename Bob was asked to write |

**Return contract — always parse with `json.loads()`:**

```json
{
  "done": true,
  "reason": "follow-up-brief.md contains all required sections.",
  "next_state": ""
}
```

On parse failure (Bob wrapped JSON in fences), recover:

```python
try:
    result = json.loads(eval_raw)
except json.JSONDecodeError:
    state = "Evaluator returned invalid JSON. Re-read the output and fix any issues."
    continue
```

---

## Adapting templates for other domains

The three templates above are written for a monthly-report comparison task. To reuse this pattern for a different domain:

1. **PLAN_PROMPT** — no changes needed; it is domain-agnostic
2. **ACT_PROMPT** — replace the file list and the three required output sections with your domain's inputs and output structure
3. **EVAL_PROMPT** — update the checklist inside "Check that `{output}` contains ALL of:" to match your output's required sections
