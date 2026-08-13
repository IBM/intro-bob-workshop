# IBM Bob Workshop for the Silicon Valley Leadership Group
## Meet Bob: Agentic AI in Action

## Workshop Overview

This workshop introduces IBM Bob — an agentic AI assistant — to audiences outside IBM. Whether you write code, lead a team, or teach at a university, you'll leave having built your own agent and experienced first-hand how AI can move beyond single prompts to plan, reason through data, and produce structured results autonomously.

The session opens with a whole-group demonstration, then branches into three role-based tracks where each participant builds an agent relevant to their work. The workshop closes with a participant-driven agent design activity and group discussion.

**Duration:** 60 minutes guided workshop (following a 30-minute presentation)

**Target Audience:** Mixed — software developers, product managers, executives, and college-level educators/professors

**Prerequisites:** None. Laptop with Bob access and VS Code with the Bob extension. Don't have Bob yet? [Download the free trial at bob.ibm.com/download](https://bob.ibm.com/download).

**Materials Needed:** Laptop with Bob access, VS Code with Bob extension, projector for shared demos

---

## Workshop Agenda

| Segment | Time |
| :--- | :--- |
| Warm-Up: Whole-Group Exercise | 10 minutes |
| Track Exercises (choose your track) | 20 minutes |
| Participant-Driven Activity | 20 minutes |
| Discussion and Q&A | 10 minutes |
| **Total** | **60 minutes** |

---

## What is Agentic AI?

### Traditional AI vs. Agentic AI

**Traditional AI Assistants:**

- Answer questions and provide information
- Generate text or code on request
- Offer suggestions and recommendations
- Passive — they respond but don't act

**Agentic AI (IBM Bob):**

- **Autonomous action:** Takes initiative to complete multi-step tasks
- **Tool usage:** Reads, writes, and modifies files independently
- **Multi-step reasoning:** Breaks complex problems into executable steps
- **Context awareness:** Understands your project structure and relationships
- **Iterative refinement:** Adapts based on results and feedback

**Key Differentiator:** Bob doesn't just suggest — Bob executes, creating tangible deliverables.

---

## How an Agent Thinks

Every agent — no matter how complex — follows the same four-step loop. Understanding this loop is what separates agentic AI from a simple chatbot.

| Stage | What it does | Monthly-report example |
| :--- | :--- | :--- |
| **Plan** | Decides what to do and in what order | "I need to read last month's report, then this month's, then compare them line by line." |
| **Act** | Uses a tool or reads/writes a file to carry out one step | Reads both report files from disk. |
| **Evaluate** | Checks whether the result is complete or needs more work | Reviews each item and labels it: *completed*, *still pending*, or *new issue*. |
| **Output** | Delivers the final result — or loops back if something is missing | Writes a follow-up action brief listing every open item with an owner and due date. |

The loop can run once or dozens of times before the agent is satisfied it has answered the question. That self-checking behavior — *evaluate and retry* — is the key difference between an agent and a one-shot prompt.

---

## Part 1: Warm-Up — Whole-Group Exercise (10 minutes)

Everyone does this together. The goal is a quick, impressive demonstration that shows the whole room what Bob is capable of before participants branch into their own tracks.

### Exercise 1: "Build Me a Dashboard"

**Objective:** See Bob go from a plain-language description to a working, interactive file in a single prompt.

**Task — type this into Bob:**

```
Create a self-contained interactive HTML dashboard that:
- Shows 5 made-up employees with their name, department, and performance score (1–10)
- Displays the data as a sortable table
- Has a bar chart showing scores by department
- Includes a summary card showing average score, highest performer, and lowest performer
- Uses a clean, professional look — no external libraries, fully self-contained

Save it as "team-dashboard.html"
Then give me the file path so I can open it in my browser.
```

**What to observe:**

- Bob creates a complete, working HTML file with no setup required
- Bob writes the chart, table, and summary logic all at once
- The file opens directly in a browser — no server, no install
- Bob narrates every step it takes

**Facilitator note:** Open the file live in a browser so the whole room can see it work. This is the "wow" moment — don't skip it.

**Quick discussion (2 minutes):**

- What just happened? What did Bob *actually* do?
- How long would that have taken to build manually?
- What would you change about it?

### Exercise 2: Iterate on the Dashboard

The first prompt got you something working. Now see what happens when you ask Bob to improve it. Try one of the prompts below — or write your own.

**Example follow-up prompts:**

```
Can you add a filter so I can show only the Engineering department?
```

```
Add a slider that filters out anyone with a performance score below a certain level.
```

```
Make the bar chart color-coded — green for scores above 7, yellow for 5–7, red for below 5.
```

```
Add a search box so I can look up an employee by name.
```

**What to observe:**

- Bob reads and understands the file it already created — you don't need to re-explain it
- A single follow-up sentence produces a targeted, working change
- The rest of the dashboard stays intact; Bob only touches what it needs to

**Facilitator note:** Let a participant call out one change they want to see and run it live. This demonstrates that the first output is just a starting point — not a finished product you hand off and walk away from.

---

## Part 2: Guided Track Exercises (20 minutes)

Participants choose the track that fits their role. Each track takes approximately 20 minutes.

---

### 🖥️ Track A: Software Developers

**Audience:** Software engineers, architects, DevOps practitioners, data engineers

**Objective:** Use Bob to build a fully runnable Python agent that reads two monthly reports, compares them, and produces a structured follow-up brief — demonstrating the Plan → Act → Evaluate → Output loop in live, executable code.

!!! note "Before starting Exercise A1"
    Click **New Task** in Bob to clear the context window from Part 1. This ensures Bob isn't influenced by the previous request.

#### Exercise A1: Build a Report Comparison Agent

**Task:**

```
Build a Python report comparison agent. The agent should:

1. First, create two plain-text files in a folder called "report-agent":
   - "report_last_month.txt" — a fictional project status report for last month
     with 8 items (mix of completed work, ongoing tasks, and blockers)
   - "report_this_month.txt" — a fictional status report for this month
     referencing some of the same items (some now completed, some still open,
     some new)

2. Then write a Python script called "agent.py" in the same folder that
   implements a genuine Plan → Act → Evaluate → Output loop:

   PLAN: For each item found in the reports, decide what needs to be checked.

   ACT: Classify each item as COMPLETED, STILL PENDING, or NEW ISSUE by calling
   the Ollama API (http://localhost:11434/api/generate, model "llama3") with a
   short prompt that passes in the item text and asks for a one-word classification
   and a one-sentence reason. If Ollama is not running (connection refused), fall
   back to keyword matching and record "[fallback: Ollama unavailable]" in the
   trace for that item.

   EVALUATE: After classifying all items, check whether fewer than 2 actionable
   items (STILL PENDING or NEW ISSUE) were found. If so, retry the ACT step with
   a broader prompt that asks the model to be more inclusive, and record the
   retry decision in the trace (e.g., "Only 1 actionable item found — retrying
   with broader criteria...").

   OUTPUT: Build a list of execution trace entries as the loop runs — one entry
   per item — recording: the item text, the classification, the model's reason
   (or fallback note), and whether it came from a retry. Then generate a
   self-contained HTML file called "report.html" that:
     - Opens automatically in the default browser when the script finishes
     - Has two sections side by side: a "Decision/Execution Trace" panel on the
       left and the final results on the right
     - The Decision/Execution Trace panel replays the trace entries one at a time
       using a CSS animation (each step fades in 0.4 s after the previous),
       so the audience watches each classification decision appear in sequence
     - Each trace entry shows: the item name, the classification badge, and the
       model's one-sentence reason (or fallback note in italics)
     - If the retry loop fired, its entry appears highlighted in amber so it
       stands out as the self-correction moment
     - The results panel shows a summary card (total / completed / pending /
       new issues) and a color-coded table: green for COMPLETED, amber for
       STILL PENDING, red for NEW ISSUE
     - Includes a "Follow-up Action Brief" below the table listing only
       STILL PENDING and NEW ISSUE items, each with a suggested next step
     - Uses clean, professional styling — no external libraries or CDN links,
       fully self-contained

3. Include a short README.md explaining what the agent does, how to run it,
   and how to start Ollama locally if needed (`ollama run llama3`).

Use only Python standard library for everything except the Ollama HTTP call
(use urllib.request — no pip installs required).
Save everything in a folder called "report-agent".
```

**Run it:**

In the VS Code integrated terminal, run these as two separate commands:

1. Navigate into the folder:
    ```bash
    cd report-agent
    ```
2. Run the script:
    ```bash
    python agent.py
    ```

`report.html` will open in your browser automatically. Watch the left panel — each classification decision appears one by one, with the model's reason, as the agent works through the reports.

**What to observe:**

- The **left panel is a Decision/Execution Trace** — each entry shows the item, the classification, and the model's stated reason. This is the Act step happening at runtime, not pre-computed output
- If Ollama wasn't running, entries marked *[fallback: Ollama unavailable]* show the keyword-matching path — a concrete illustration of graceful degradation
- If the retry fired, watch for the **amber highlight**: the agent evaluated its own output, decided it wasn't good enough, and re-ran — that's the Evaluate step made visible
- The **right panel** shows the color-coded classification table and follow-up brief — the Output step: the structured artifact the agent produced after reasoning through every item
- Bob wrote the Ollama integration, the retry loop, the fallback path, the execution trace, *and* the animated HTML from a single natural-language description

**Follow-up prompt (if time allows):**

```
Add a confidence score (0–100) to each reasoning step and each row
in the results table. Show it as a small color-matched badge.
The score should reflect how clearly the item's status changed
between the two reports.
```

**Discussion points:**

- At what point in the Decision/Execution Trace did you see the agent *evaluate* its own output before continuing?
- How would you extend this agent to pull reports from a real system (Jira, Confluence, email)?
- What parts of this output would you trust immediately, and what would you verify before sending to a stakeholder?
- How does building this — the logic, the retry loop, and the animated report — compare to writing it from scratch without Bob?

---

### 📋 Track B: Product Managers and Executives

**Audience:** PMs, product owners, directors, VPs, executives, business analysts

**Objective:** Direct Bob to build and run a project status comparison agent — no code required. You define the agent's role through natural language; Bob handles the implementation and execution inside VS Code. You experience the agentic loop through the decisions the agent makes on your behalf.

!!! note "Before starting Exercise B1"
    Click **New Task** in Bob to clear the context window from Part 1. This ensures Bob isn't influenced by the previous request.

!!! tip "You are the agent designer, not the coder"
    In this track you write the prompts that define what the agent does. Bob builds it, runs it, and brings you the result. Your job is to evaluate what the agent decided and refine its instructions — the same skills you use every day as a PM.

#### Exercise B1: Build a Status Report Comparison Agent

**Task:**

```
I want to build an agent that compares monthly project status reports and
tells me what to follow up on. Please:

1. Create two fictional project status reports as plain-text files:
   - "status_june.txt" — last month's report with 8 project items
     (a mix of completed milestones, ongoing work, and risks/blockers)
   - "status_july.txt" — this month's report referencing the same project
     (some items resolved, some still open, some new issues added)

2. Build a Python agent called "status_agent.py" that:
   - Reads both reports
   - Compares them and classifies each item as: DONE, STILL OPEN, or NEW ISSUE
   - Explains its reasoning for each classification in plain English
   - Produces a clean follow-up action brief saved as "action_brief.txt"
     with only the STILL OPEN and NEW ISSUE items, each with a suggested owner
     and suggested next step

3. Run the agent and show me the action_brief.txt when it's done.

Save everything in a folder called "status-agent".
```

**What to observe:**

- Watch Bob's narration as it builds the agent — this is the **Plan** stage made visible
- The agent's reasoning explanation is the **Evaluate** stage: it is checking its own classifications before committing them to the brief
- `action_brief.txt` is a business artifact the running agent produced autonomously — not written by Bob in chat, but generated by code that reasoned through the data
- Notice what the agent inferred *without being told*: owner suggestions, next-step wording, item grouping

**Follow-up prompts (if time allows):**

```
Now show me the action brief as a formatted table in chat — columns for
Item, Status, Suggested Owner, and Next Step.
```

```
Re-run the status agent but this time only include items that have been
STILL OPEN for more than one reporting period. Add a "Priority" field to
each item in action_brief.txt: High if it's a blocker or risk, Medium otherwise.
```

**Discussion points:**

- What did the agent decide that you would have decided differently? Why?
- How would this change your weekly status review process?
- Where does human PM judgment still own the decision — and where is the agent genuinely useful?
- What would you need to trust before sending the agent's output directly to a stakeholder?

---

### 🎓 Track C: College Professors and Educators

**Audience:** University faculty, instructors, curriculum designers, academic researchers

**Objective:** Direct Bob to build and run a student submission review agent — no code required. You define the evaluation criteria through natural language; Bob builds the agent and runs it. You experience the agentic loop through the triage decisions it makes, and decide where your instructor judgment still needs to take over.

!!! note "Before starting Exercise C1"
    Click **New Task** in Bob to clear the context window from Part 1. This ensures Bob isn't influenced by the previous request.

!!! tip "The agent triages — you decide"
    This agent does not grade. It reads student responses against the rubric you define, flags what needs attention, and hands the decision back to you. Your expertise is still the final word.

#### Exercise C1: Build a Student Submission Review Agent

**Task:**

```
I want to build an agent that helps me triage student short-answer responses
before I read them. Please:

1. Generate 5 fictional student responses (2–4 paragraphs each) to the
   following prompt:
   "Describe one real-world example of agentic AI and explain what makes
   it different from a traditional AI assistant."
   Save them as "student_1.txt" through "student_5.txt" in a folder
   called "review-agent". Make the responses vary in quality — some strong,
   some that miss key concepts, one that is off-topic.

2. Build a Python agent called "review_agent.py" that:
   - Reads each student response file
   - Evaluates it against this rubric:
       * Criterion 1: Identifies a real and plausible real-world example (0–2 points)
       * Criterion 2: Correctly explains what makes agentic AI different (0–2 points)
       * Criterion 3: Writing is clear and on-topic (0–1 point)
   - Classifies each submission as: STRONG, NEEDS REVISION, or NEEDS INSTRUCTOR ATTENTION
   - Flags any submission it is uncertain about with "[REVIEW RECOMMENDED]"
   - Builds a reasoning trace as it works — one entry per student — capturing
     what it found against each criterion and why it made the classification
   - Generates a self-contained HTML file called "triage_report.html" that:
     - Opens automatically in the default browser when the script finishes
     - Has two sections side by side: an "Agent Reasoning" panel on the left
       and the triage results on the right
     - The Agent Reasoning panel replays the reasoning steps one at a time
       using a CSS animation (each step fades in 0.4s after the previous),
       so you can watch the agent evaluate each student in sequence
     - Any step where the agent flags uncertainty appears highlighted in amber
       so the self-correction moment stands out
     - The results panel shows a summary card at the top (total submissions,
       how many STRONG, NEEDS REVISION, NEEDS INSTRUCTOR ATTENTION)
     - Below the summary, a color-coded table — one row per student:
       green for STRONG, amber for NEEDS REVISION, red for NEEDS INSTRUCTOR ATTENTION
     - Each red row shows a visible "REVIEW RECOMMENDED" badge if flagged
     - Each row includes the total score and a one-sentence agent note
     - Uses clean, professional styling — no external libraries or CDN links,
       fully self-contained

3. Include a short README.md explaining what the agent does and how to run it.

Use only Python standard library — no pip installs required.
Save everything in a folder called "review-agent".
```

**Run it:**

In the VS Code integrated terminal, run these as two separate commands:

1. Navigate into the folder:
    ```bash
    cd review-agent
    ```
2. Run the script:
    ```bash
    python review_agent.py
    ```

`triage_report.html` will open in your browser automatically. Watch the left panel — the agent works through each student one at a time before the final triage table appears on the right.

**What to observe:**

- The **left panel animates the reasoning** per student — watch the agent apply each rubric criterion in sequence before committing to a classification
- The **amber highlight** marks where the agent flagged its own uncertainty — this is the Evaluate stage made visible, the agent recognizing the limits of its confidence
- The **REVIEW RECOMMENDED badge** on red rows tells you exactly where your reading time is most needed before you open a single document
- The color-coded table gives you a scannable triage view of the whole class at a glance
- Notice how the rubric you wrote in plain English was interpreted and applied consistently — you specified the criteria, not the algorithm

**Follow-up prompt (if time allows):**

```
Re-run the review agent with a revised rubric: add a fourth criterion —
"Criterion 4: Response demonstrates original thinking beyond the lecture
slides (0–2 points)."
Update the classification thresholds accordingly and regenerate
triage_report.html.
```

**Discussion points:**

- Which classifications would you have made differently? What does that tell you about the rubric?
- Where did the agent add the REVIEW RECOMMENDED flag, and do you agree with those choices?
- How would you explain this kind of AI-assisted triage to students — and to your department?
- What is the risk of over-trusting a triage agent in an academic context? How do you guard against it?

---

## Part 3: Participant-Driven Activity (20 minutes)

!!! note "Before starting Part 3"
    Click **New Task** in Bob to clear the context window from your track exercise. You're starting something new — a clean context gives Bob a fresh start.

Now it's your turn. Design and build your own agent — one that solves a problem you actually have, or one you've always wanted to automate. It doesn't need to be production-ready; the goal is to go through the full design loop yourself.

### Your Agent Design Canvas

Before you prompt Bob, answer these four questions. Write them down or just keep them in mind — they are the skeleton of your prompt.

| Question | Your answer |
| :--- | :--- |
| **Role** — What is this agent's job? | e.g., "An agent that reviews my team's weekly updates" |
| **Inputs** — What does it read? | e.g., "Five plain-text update files, one per team member" |
| **Decision** — What does it classify or decide? | e.g., "Flag items that are blocked or overdue" |
| **Output** — What artifact does it produce? | e.g., "A summary table with action items and owners" |

### Instructions

- **5 minutes:** Fill in the canvas above for a problem that interests you. See the examples below for inspiration.
- **10 minutes:** Turn your canvas into a prompt and ask Bob to build and run the agent.
- **5 minutes:** Review the output. Ask Bob to adjust one thing the agent decided — change a threshold, add a criterion, or change the output format. Note what changed.

### Prompt-Writing Tips

- Lead with the agent's role: *"Build an agent that…"*
- Specify the inputs explicitly — tell Bob what files to create as sample data
- Describe the decision in terms of categories or classifications the agent should produce
- Ask Bob to show its reasoning, not just the final output
- Ask Bob to run the agent and show you the result — don't just ask for the code

### Example Starting Points by Role

**For developers:**
```
Build an agent that reads [N] sample [log files / pull request descriptions / test results]
and classifies each as [needs attention / looks good / needs review].
Have it print a reasoning trace and save a summary to "[filename]".
Save everything in "[folder-name]".
```
*Example: "Build an agent that reads 5 sample pull request descriptions and classifies each as
Ready to Merge, Needs Changes, or Needs Architect Review. Print the reasoning for each and
save a summary to 'pr-triage.txt'. Save in 'pr-agent/'."*

**For PMs and execs:**
```
Build an agent that reads [N] sample [status updates / meeting notes / customer feedback items]
and produces a [prioritized action list / risk summary / follow-up brief].
Have it explain why it flagged each item. Save the output to "[filename]".
```
*Example: "Build an agent that reads 4 sample customer feedback entries and classifies each as
Quick Win, Needs Investigation, or Escalate. Explain each classification and save a brief to
'feedback-triage.txt'."*

**For professors:**
```
Build an agent that reads [N] sample [student reflections / discussion posts / assignment drafts]
and evaluates each against this rubric: [your criteria].
Classify each as [Strong / Needs Revision / Needs Attention] and save a triage report to "[filename]".
```
*Example: "Build an agent that reads 4 sample student discussion posts on AI ethics and evaluates
each for: (1) clarity of argument, (2) use of evidence, (3) originality. Classify each and save a
triage report to 'discussion-triage.txt'."*

### Facilitator Discussion Prompts

Once participants have their agents, bring the room back together and ask:

- What agent did you design, and what problem does it solve?
- What decision did the agent make that surprised you — or that you disagreed with?
- What would you need to change in the agent's instructions to get a better result?
- Where does the agent save you time, and where does your judgment still matter?
- Would you actually use this agent in your work? What would make it trustworthy enough?

---

## Part 4: Discussion and Q&A (10 minutes)

Invite 3–4 participants to share:

- What agent they designed, and what problem it was meant to solve
- A decision the agent made that surprised them — or that they would have made differently
- One place where the agent was genuinely useful, and one place where they would not trust it without review
- Whether they'd actually use or adapt the agent in their real work

Then open for Q&A. Common questions to be ready for:

**"Is this safe to use at my company?"**
The Bob extension runs inside VS Code on your machine, but your prompts are sent to a remote model endpoint to generate responses — they do not stay local. How that data is handled depends on which model your organisation has configured and the terms of your enterprise agreement with that provider. Always check your company's AI usage guidelines before using any AI tool with proprietary information.

**"How do I know if the output is correct?"**
You don't — without reviewing it. The agent is a strong starting point, not a final decision. Always apply your domain expertise to validate what the agent produces before acting on it.

**"Can Bob connect to the internet or my company's systems?"**
Not by default. Bob works with local files and tools. Integrations with external systems require configuration.

**"What makes Bob different from a general-purpose chat tool?"**
Bob is an *agentic* AI — it doesn't just answer questions. It follows a Plan → Act → Evaluate → Output loop: it decides what steps to take, uses tools to carry them out, checks whether the result is complete, and either delivers the output or tries again. General-purpose chat tools can answer questions about code; Bob is embedded in your IDE and acts directly on your workspace — reading, writing, and running files as part of its reasoning loop. The agentic behaviour isn't a feature you configure; it's how Bob works by default.

---

## Key Takeaways

This workshop aligns with the Silicon Valley Leadership Group's Agentic AI Task Force focus on practical, responsible adoption. Participants leave having built agents that plan, act, evaluate, and output — and having experienced first-hand where those agents add genuine value and where human judgment still owns the decision.

### For Everyone

- **Agents don't just respond — they reason** — the Plan → Act → Evaluate → Output loop is what separates an agent from a chatbot
- **Natural language is the interface** — you define the agent's role, inputs, and decisions in plain English; no code required for most tracks
- **The agent's output is a starting point** — always review what it decided before acting on it
- **Iteration is fast** — adjusting one instruction in the agent's definition changes every decision it makes

### For Developers

- Bob can scaffold a fully runnable agent from a natural language description — the reasoning loop is visible in the code and in the terminal output
- Focus shifts from writing classification and comparison logic from scratch to reviewing and refining agent behavior
- The hardest part of agent design is not the code — it is defining the right decision criteria clearly enough for an agent to apply them consistently

### For PMs and Executives

- An agent that reads, compares, and classifies report data can compress hours of weekly status review into minutes
- The value of the agent is in the decisions it surfaces — your job is to evaluate those decisions, not to produce them
- Human judgment on strategy, priorities, and stakeholder context remains irreplaceable — agents triage, humans decide

### For Professors and Educators

- A triage agent applies a rubric consistently across every submission — that consistency is its main value, not its judgment
- AI-assisted triage tells you where to spend your reading time; it does not replace reading
- Explaining how and why you use AI tools to students is itself a meaningful teaching moment about responsible AI adoption

---

## Best Practices

### Do's ✅

- **Define the agent's decision clearly** — the more precisely you describe what the agent should classify or decide, the more consistent its output will be
- **Ask Bob to show its reasoning** — tell the agent to print or log why it made each decision, not just what it decided
- **Specify inputs explicitly** — tell Bob what sample files to create so the agent has something concrete to work with
- **Iterate on the agent's instructions** — treat the first run as a calibration; adjust one criterion at a time and re-run

### Don'ts ❌

- **Don't skip review** — agents can make consistent mistakes; always apply your expertise before acting on the output
- **Don't include sensitive data** — avoid putting confidential, proprietary, or personal data in prompts
- **Don't treat the agent's output as a final decision** — agents classify and surface; humans decide and act
- **Don't over-specify the implementation** — describe what the agent should decide, not how to write the code; give Bob the goal and let it work

---

## Facilitator Guide

### Pre-Workshop Setup

- Verify all participants have Bob installed and working in VS Code before the session starts
- Test the warm-up dashboard prompt yourself in advance — confirm it works in your environment
- For Track A (developers): confirm Python is available on their machines (`python --version` or `python3 --version` in the terminal)
- Have the track exercise prompts available in a shared document so participants can copy-paste rather than type
- Identify which participants are likely in each track (ask in advance if possible)
- Have 2–3 backup agent ideas ready for Part 3 in case anyone is stuck on what to build

### Timing Tips

- The warm-up exercise (Part 1) is the most important segment — don't rush it and don't skip opening the result in a browser
- During Track A, circulate and help anyone whose terminal is not working — the exercise depends on running the script
- During Tracks B and C, remind participants they do not need to read or understand the code — they are evaluating the agent's decisions
- For Part 3, give a 5-minute warning so participants can wrap up before the group discussion
- The Q&A segment is flexible — expand it if energy is high, use it to do a second participant agent demo if energy is low

### Managing Mixed Ability

- Encourage developers who finish Track A early to add the confidence scoring follow-up, or start designing their Part 3 agent
- For participants who are less technical, remind them that Tracks B and C require no code knowledge — their job is to evaluate the agent's decisions, which is a judgment skill they already have
- Remind everyone that the agent design canvas (role / inputs / decision / output) works for any level of technical background

### Success Criteria

The workshop is successful if participants leave able to:

- Articulate the difference between a one-shot prompt and an agent with a Plan → Act → Evaluate → Output loop
- Describe at least one agent they could build for a real problem in their own work
- Explain where an agent adds value and where human judgment still owns the decision

---

## Advanced Optional Lab: Data Science Lab

Want to go deeper? Work through the full step-by-step data science lab built by the IBM Bob field team. You'll discover how to use Bob to:

Perform data analysis
Create interactive dashboards using Jupyter notebooks
Build web applications with Streamlit

👉 [IBM Bob Data Science Lab (step-by-step)](https://github.ibm.com/code-assistant/bob-field-demos/blob/master/datascience-lab/lab/step-by-step-lab.md)

This is a great next step if you finished the track exercises early, or want to continue exploring after the workshop.
