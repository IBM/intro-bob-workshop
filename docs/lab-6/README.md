# IBM Bob Workshop for the Silicon Valley Leadership Group
## Meet Bob: Agentic AI in Action

## Workshop Overview

This workshop introduces IBM Bob — an agentic AI assistant — to audiences outside IBM. Whether you write code, lead a team, or teach at a university, you'll leave having built your own agent and experienced first-hand how AI can move beyond single prompts to plan, reason through data, and produce structured results autonomously.

The session opens with a whole-group demonstration, then branches into three role-based tracks where each participant builds an agent relevant to their work. The workshop closes with a participant-driven agent design activity and group discussion.

**Duration:** 60 minutes guided workshop (following a 30-minute presentation)

**Target Audience:** Mixed — software developers, product managers, executives, and college-level educators/professors

**Prerequisites:** None. Laptop with Bob access and Bob IDE. Don't have Bob yet? [Download the free trial at bob.ibm.com/download](https://bob.ibm.com/download).

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

| Stage | What it does | [Monthly-report example](#exercise-a1-build-a-report-comparison-agent) |
| :--- | :--- | :--- |
| **Plan** | Decides what to do and in what order — describes the single next action without executing it | "I need to read `january.md` and `february.md`, then compare them item by item. I will not execute this yet." |
| **Act** | Uses a tool or reads/writes a file to carry out exactly one step of the plan | Reads `january.md` and `february.md` from disk and writes the structured comparison output to a file. |
| **Evaluate** | Checks whether the goal is fully achieved; returns `done: true` or `done: false` with a reason and the next state to feed back into Plan | Reviews the comparison output and confirms every status item is labelled *Completed*, *Pending*, or *New*. If anything is missing, sets `done: false` and describes what still needs to be done. |
| **Output** | Delivers the final result — or loops back into Plan if Evaluate said the work is incomplete | Writes a follow-up action brief (rendered in the web UI) listing every open item; if the brief is incomplete, the loop restarts at Plan. |

The loop can run once or dozens of times before the agent is satisfied it has answered the question. That self-checking behavior — *evaluate and retry* — is the key difference between an agent and a chatbot that responds once and stops.

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

!!! info "Learn Agentic AI Concepts—By Having Bob Build Them for You!"
    The core purpose of this workshop is two-fold: introducing **Bob as a powerful code agent** (your automated developer teammate), and learning **how real-world AI agents actually work** (how they plan, reason, and take action).
    
    Instead of spending your time writing tedious boilerplate code or configuring complex development environments to build an agent, you will design the agent's role and rules in plain English. Bob will then act as your developer—instantly translating your high-level ideas into a fully running, interactive agent application that you can take home!
    
    To make this experience simple and accessible, we will use a custom skill we have prepared for you (like `agent-with-bob-shell`). This skill empowers Bob to act as a highly capable software engineer, letting you focus on **conceptual agent design**—defining the rules, triaging the reasoning, and observing the core agentic loop (Plan → Act → Evaluate → Output) in action.
    
    *If you are interested in how custom skills work or want to learn how we wrote this skill to help others ease into agentic AI, you can explore the [Custom Skill Definition](https://github.com/ibm/intro-bob-workshop/blob/master/.bob/skills/agent-with-bob-shell/SKILL.md) and [Examples](https://github.com/ibm/intro-bob-workshop/blob/master/.bob/skills/agent-with-bob-shell/EXAMPLES.md).*

### 🚀 Step-by-Step Workspace Skill Setup

To use the workshop's custom skills (such as `agent-with-bob-shell`) in Bob, your active workspace folder needs to contain the `.bob` directory.

You can download and extract **only** the `.bob/` folder directly into your current workspace with a single terminal command:

**On macOS / Linux:**
Open the integrated terminal in your current workspace and run:
```bash
curl -L https://github.com/ibm/intro-bob-workshop/archive/refs/heads/main.tar.gz | tar -xz --strip-components=1 "intro-bob-workshop-main/.bob"
```

**On Windows (PowerShell):**
Open PowerShell in your current workspace and run:
```powershell
Invoke-WebRequest -Uri "https://github.com/ibm/intro-bob-workshop/archive/refs/heads/main.zip" -OutFile "temp.zip"; Expand-Archive -Path "temp.zip" -DestinationPath "temp_extracted"; Move-Item -Path "temp_extracted\intro-bob-workshop-main\.bob" -Destination ".bob"; Remove-Item -Recurse -Force "temp.zip", "temp_extracted"
```

Once the command finishes, your current workspace will have the custom skills directory ready, and you can immediately start prompting your code agent!

---

### 🖥️ Track A: Software Developers

**Audience:** Software engineers, architects, DevOps practitioners, data engineers

**Objective:** Use Bob to build a fully runnable Python agent that reads two monthly reports, compares them, and produces a structured follow-up brief — demonstrating the Plan → Act → Evaluate → Output loop in live, executable code.

!!! note "Before starting Exercise A1"
    Click **New Task** in Bob to clear the context window from Part 1. This ensures Bob isn't influenced by the previous request.

#### Exercise A1: Build a Report Comparison Agent

**Task:**

```
/agent-with-bob-shell create an agent application that compares monthly
project status reports and tells me what to follow up on. Also generate
two sample monthly project status reports I can use for testing. The
application should provide a web interface for a better user experience.
Put the whole project under a folder called `monthly-report-agent` in
this workspace.
```

**Run it:**

In the VS Code integrated terminal, run these as two separate commands:

1. Navigate into the folder:
    ```bash
    cd monthly-report-agent
    ```
2. Run the script:
    ```bash
    python server.py
    ```

Follow the on-screen instructions to open the app (typically running on `http://127.0.0.1:5001`).

**What to observe:**

- **Interactive Web Interface:** Instead of a static file, Bob has generated a fully interactive web application with standard styling, enabling a smoother user experience.
- **Sample Report Files Created:** Verify that the two sample status reports (e.g. `reports/january.md` and `reports/february.md`) were successfully created inside the `monthly-report-agent` folder.
- **Dynamic Comparison via File Upload:** Drag and drop or upload these two generated report files into the web interface's upload boxes and click "Run Analysis" to perform the comparison.
- **Analysis and Follow-up Actions:** The web UI clearly classifies each status item (Completed, Pending, or New) and generates clear, actionable follow-up recommendations.
- **End-to-End Delivery:** Bob designed the comparison logic, built the routing and styling for the web interface, and created the sample data files starting from a single, simple prompt.

**Follow-up prompt (if time allows):**

```
Add a search bar and status filter (e.g. Completed, Pending, New)
to the web interface so I can quickly find specific items in the list.
```

**Discussion points:**

- What makes this application a genuine AI agent rather than a typical script or a simple LLM wrapper? (Hint: Think about the agent's tool-use, planning, and decision-making capabilities.)
- How does having Bob automatically generate sample status files speed up your prototyping and testing cycle?
- How do specialized skills (like `agent-with-bob-shell`) change how we package and share repeatable agentic workflows or development tasks with others?

---

### 📋 Track B: Product Managers and Executives

**Audience:** PMs, product owners, directors, VPs, executives, business analysts

**Objective:** Direct Bob to build and launch an interactive web application that compares project status reports — no coding required. Using Bob's custom skill (`agent-with-bob-shell`), you define what you need in plain English, and watch Bob build, run, and host the dashboard on your behalf.

!!! note "Before starting Exercise B1"
    Click **New Task** in Bob to clear the context window from Part 1. This ensures Bob isn't influenced by the previous request.

!!! tip "You are the product owner, not the developer"
    In this track, you write requirements in plain English. Bob acts as your engineering partner—writing the code, creating the reports, and launching the application. Your job is to evaluate the resulting web app and request refinements, just like reviewing a product prototype with your engineering team.

#### Exercise B1: Build a Status Report Comparison Agent

**Task:**

```
/agent-with-bob-shell create an agent application that compares two fictional project status reports as plain-text files:
   - "status_june.txt" — last month's report with 8 project items
     (a mix of completed milestones, ongoing work, and risks/blockers)
   - "status_july.txt" — this month's report referencing the same project
     (some items resolved, some still open, some new issues added).

The application should provide a web interface for a better user experience.
Put the whole project under a folder called `project-report-agent` in this workspace.
```

**What to observe:**

- **How Bob Plans in Chat:** Watch Bob's thought process as it details exactly how it will build the application based on your natural language request.
- **Automated Mock Data:** Notice how Bob automatically writes realistic project status files (`status_june.txt` and `status_july.txt`) so you have sample data for testing right away.
- **Visual Interface Design:** Observe how Bob designs and builds a clean web dashboard with upload areas, status badges (Done, Still Open, New Issue), and clear comparison tables.
- **Zero-Code Delivery:** You didn't have to write code, configure servers, or build pages. Bob handled the implementation end-to-end and handed you a fully interactive business tool.

**Follow-up prompts (if time allows):**

```
Add a summary card at the top of the webpage that shows key stats:
total number of items, how many are completed, and how many are still open.
```

```
Add a search bar and an option to filter by status (Completed, Open, New)
so I can find specific project items instantly.
```

**Discussion points:**

- **AI Decision Making:** Did the agent classify items correctly based on the monthly reports? What did it catch or assume that you would have evaluated differently?
- **Workflow Efficiency:** How would having an interactive comparison dashboard like this change your team's weekly or monthly status review process?
- **Human vs. AI Ownership:** Where does human project manager judgment still need to own the final decision—and where is the agent genuinely saving you time?
- **Trust and Adoption:** What kind of accuracy or safeguards would you need before trusting this tool to generate draft updates directly for VPs or external stakeholders?

---

### 🎓 Track C: College Professors and Educators

**Audience:** University faculty, instructors, curriculum designers, academic researchers

**Objective:** Direct Bob to build and launch an interactive student triage web dashboard — no coding required. Using Bob's custom skill (`agent-with-bob-shell`), you define the evaluation rubric in plain English, and watch Bob build and run a visual triage application that highlights which student submissions need your direct attention.

!!! note "Before starting Exercise C1"
    Click **New Task** in Bob to clear the context window from Part 1. This ensures Bob isn't influenced by the previous request.

!!! tip "The agent triages — you decide"
    This agent does not grade. It reads student responses against the rubric you define, flags what needs attention, and hands the decision back to you. Your expertise is still the final word.

#### Exercise C1: Build a Student Submission Review Agent

**Task:**

```
/agent-with-bob-shell I want to build an agent that helps me triage student short-answer responses
before I read them.

Please:
1. Generate 5 fictional student responses (2–4 paragraphs each) to the
   following prompt:
   "Describe one real-world example of agentic AI and explain what makes
   it different from a traditional AI assistant."
   Save them as "student_1.txt" through "student_5.txt" in a folder
   called "review-agent". Make the responses vary in quality — some strong,
   some that miss key concepts, one that is off-topic.

2. The agent should:
   - Reads each student response file
   - Evaluates it against this rubric:
       * Criterion 1: Identifies a real and plausible real-world example (0–2 points)
       * Criterion 2: Correctly explains what makes agentic AI different (0–2 points)
       * Criterion 3: Writing is clear and on-topic (0–1 point)
   - Classifies each submission as: STRONG, NEEDS REVISION, or NEEDS INSTRUCTOR ATTENTION
   - Flags any submission it is uncertain about with "[REVIEW RECOMMENDED]"
   - Builds a reasoning trace as it works — one entry per student — capturing
     what it found against each criterion and why it made the classification

The application should provide a web interface for a better user experience.
Put the whole project under a folder called `review-agent` in this workspace.
```

**Run it:**

In the VS Code integrated terminal, run these as two separate commands:

1. Navigate into the folder:
    ```bash
    cd review-agent
    ```
2. Run the script:
    ```bash
    python server.py
    ```

Follow the on-screen instructions to open the app (typically running on `http://127.0.0.1:5001`).

**What to observe:**

- **Automated Triage Assistant:** Observe how Bob designs and builds a clean grading dashboard, letting you easily review and organize student responses visually.
- **Realistic Sample Material:** Verify that the 5 fictional student essays (`student_1.txt` to `student_5.txt`) varying in quality were successfully created inside the `review-agent` folder.
- **Identify Actionable Submissions:** Note where the agent flags submissions as `NEEDS INSTRUCTOR ATTENTION` or `[REVIEW RECOMMENDED]`, helping you instantly see where your direct feedback is most needed.
- **No-Code Implementation:** You designed a fully functional teaching tool with natural language—letting Bob manage folders, write comparison scripts, and build interactive webpages.

**Follow-up prompt (if time allows):**

```
Add a text input box to the web interface so I can add new student responses
directly from the browser and have them analyzed.
```

**Discussion points:**

- **Assessing AI Judgment:** Did the agent's web dashboard score the student essays correctly? Where did your professional grading judgment disagree with the AI's triage?
- **Academic Safeguards:** What is the risk of over-trusting an AI triage tool when grading or providing academic feedback? How do you guard against it?
- **Transparency and Communication:** How would you explain this kind of AI-assisted grading and triage system to your students and your academic department?

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
Bob IDE runs on your machine, but your prompts are sent to a remote model endpoint to generate responses — they do not stay local. How that data is handled depends on which model your organisation has configured and the terms of your enterprise agreement with that provider. Always check your company's AI usage guidelines before using any AI tool with proprietary information.

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
