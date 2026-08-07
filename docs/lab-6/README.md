# IBM Bob Workshop for the Silicon Valley Leadership Group
## Meet Bob: Agentic AI in Action

### Workshop Overview

This workshop introduces IBM Bob — an agentic AI assistant — to audiences outside IBM. Whether you write code, lead a team, or teach at a university, you'll leave with a concrete sense of what agentic AI can do and how it differs from a regular chatbot.

The session combines a brief whole-group exercise that everyone does together, followed by three parallel guided tracks where participants choose the path most relevant to their role. The workshop closes with a participant-driven activity and group discussion.

**Duration:** 60 minutes guided workshop (following a 30-minute presentation)

**Target Audience:** Mixed — software developers, product managers, executives, and college-level educators/professors

**Prerequisites:** None. Laptop with Bob access and VS Code with the Bob extension.

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

## Part 1: Warm-Up — Whole-Group Exercise (10 minutes)

Everyone does this together. The goal is a quick, impressive demonstration that shows the whole room what Bob is capable of before participants branch into their own tracks.

### Exercise: "Build Me a Dashboard"

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

---

## Part 2: Guided Track Exercises (20 minutes)

Participants choose the track that fits their role. Each track takes approximately 20 minutes.

---

### 🖥️ Track A: Software Developers

**Audience:** Software engineers, architects, DevOps practitioners, data engineers

**Objective:** Experience Bob's ability to scaffold a working, testable project from a clear prompt — then iterate on it.

!!! note "Before starting Exercise A1"
    Click **New Task** in Bob to clear the context window from Part 1. This ensures Bob isn't influenced by the previous request.

#### Exercise A1: Scaffold a REST API with Tests

**Task:**

```
Create a small Node.js REST API for a task management service:
- Express.js framework
- Endpoints: GET /tasks, POST /tasks, PUT /tasks/:id, DELETE /tasks/:id
- In-memory storage (no database needed)
- Basic input validation (task must have a title)
- Error handling middleware
- A README with setup and test instructions

Save it in a folder called "task-api"
```

**What to observe:**

- Bob creates a multi-file project with sensible structure
- Bob includes validation and error handling without being told exactly how
- Bob generates a README you could actually hand to a teammate

**Follow-up prompt (if time allows):**

```
Add a Jest test file to the task-api project that tests:
- Creating a task returns 201 with the new task
- Getting all tasks returns an array
- Deleting a non-existent task returns 404
```

**Discussion points:**

- How much of the output would you use as-is in a real project?
- Where would you review most carefully before shipping?
- How does this change the "first hour" of a new feature or service?

---

!!! note "Before starting Exercise A2"
    Click **New Task** in Bob to clear the context window from Exercise A1. This ensures Bob isn't influenced by the previous request.

#### Exercise A2: Data Analysis with Python (Data Science Option)

**Audience:** Data engineers, data scientists, analysts with Python experience

**Task:**

```
Create a Python data analysis project:
- Generate a sample CSV file called "sales_data.csv" with 50 rows and columns:
  Region, Product, Units Sold, Unit Price, Sale Date
- Write a Python script called "analyze_sales.py" that:
  - Loads the CSV with pandas
  - Calculates total revenue per region
  - Finds the top-selling product by units
  - Computes month-over-month revenue trend
  - Outputs a summary report to "sales_summary.txt"
- Include a requirements.txt and instructions to run the analysis

Save everything in a folder called "sales-analysis"
```

**What to observe:**

- Bob generates realistic sample data alongside the analysis code
- Bob infers the right pandas operations from natural language
- Bob creates runnable code with installation instructions included

**Follow-up prompt (if time allows):**

```
Add a matplotlib visualization to analyze_sales.py that:
- Creates a bar chart of revenue by region
- Saves it as "revenue_by_region.png"
```

**Discussion points:**

- How does this compare to writing the same analysis from scratch?
- What would you validate before trusting the output in a real analysis?
- How could this accelerate exploratory data analysis on real datasets?

---

### 📋 Track B: Product Managers and Executives

**Audience:** PMs, product owners, directors, VPs, executives, business analysts

**Objective:** Experience Bob producing polished, structured business artifacts from a short brief — the kind of work that normally takes hours.

!!! note "Before starting Exercise B1"
    Click **New Task** in Bob to clear the context window from Part 1. This ensures Bob isn't influenced by the previous request.

#### Exercise B1: Write a One-Page Product Brief

**Task:**

```
Write a one-page product brief for the following:

Product: An AI-powered meeting summarizer for enterprise teams
- Listens to or reads meeting transcripts
- Generates action items, decisions made, and open questions
- Integrates with Slack and email
- Aimed at managers and team leads

Include:
- Problem statement (2–3 sentences)
- Target user persona
- Top 3 value propositions
- Success metrics (KPIs)
- Key risks and open questions

Keep it concise and executive-ready. Save it as "meeting-summarizer-brief.md"
```

**What to observe:**

- Bob structures the brief using standard PM sections without being told the exact format
- Bob infers realistic metrics and personas from the product description
- The output is ready to share with engineering or design partners

**Follow-up prompt (if time allows):**

```
Now write 5 user stories for the meeting summarizer in
"As a [persona], I want [goal], so that [benefit]" format.
Add 3 acceptance criteria for each story.
Format as a markdown table and save as "user-stories.md"
```

---

!!! note "Before starting Exercise B2"
    Click **New Task** in Bob to clear the context window from Exercise B1. This ensures Bob isn't influenced by the previous request.

#### Exercise B2: Build an Interactive Feedback Dashboard

**Task:**

```
Create a sample CSV file called "customer-feedback.csv" with 20 rows of made-up
customer feedback data. Include columns: Date, Customer Segment, Product Area,
Sentiment (Positive/Neutral/Negative), and Feedback Summary.

Then build a self-contained HTML dashboard called "feedback-dashboard.html" that:
- Shows all feedback in a filterable table (filter by Segment, Product Area, Sentiment)
- Shows a pie chart breaking down sentiment
- Shows a count card: total feedback, % positive, % negative
- Highlights Negative sentiment rows in red
- Requires no external libraries — fully self-contained

Give me the file path to open it in my browser.
```

**What to observe:**

- Bob generates realistic mock data AND the dashboard in one pass
- Bob wires the filters, chart, and summary cards together automatically
- The result is a shareable, browser-ready artifact with no setup

**Discussion points:**

- What kinds of real data would you drop into a dashboard like this?
- How does this change how you prepare for stakeholder reviews?
- Where does human PM judgment still matter most?

---

### 🎓 Track C: College Professors and Educators

**Audience:** University faculty, instructors, curriculum designers, academic researchers

**Objective:** See how Bob can accelerate course design, assignment creation, research scaffolding, and academic document production.

!!! note "Before starting Exercise C1"
    Click **New Task** in Bob to clear the context window from Part 1. This ensures Bob isn't influenced by the previous request.

#### Exercise C1: Design a Course Module

**Task:**

```
Design a one-week undergraduate course module on the following topic:

Course: Introduction to Artificial Intelligence
Module: "Agentic AI — When AI Takes Action"
Level: Sophomore/Junior undergraduate
Duration: One week (3 hours of class time + 2 hours of self-study)

Include:
- Learning objectives (4–5, written as measurable outcomes)
- Lecture outline (2 x 75-minute sessions with topics and time allocations)
- One in-class activity with instructions
- One take-home assignment with a grading rubric (3 criteria, 4-point scale)
- A list of 5 recommended readings or resources (real or plausible)

Save it as "ai-agents-module.md"
```

**What to observe:**

- Bob structures the module using standard instructional design conventions
- Bob writes measurable learning objectives without extra prompting
- Bob creates a complete, usable rubric that could go directly into a syllabus

**Follow-up prompt (if time allows):**

```
Write 10 multiple-choice exam questions for the "Agentic AI" module.
For each question include:
- The question stem
- Four answer choices (A–D)
- The correct answer
- A one-sentence explanation of why it is correct

Format as a markdown list and save as "exam-questions.md"
```

---

!!! note "Before starting Exercise C2"
    Click **New Task** in Bob to clear the context window from Exercise C1. This ensures Bob isn't influenced by the previous request.

#### Exercise C2: Research Literature Summary

**Task:**

```
Act as a research assistant. Write a structured literature review section
on the following topic for a computer science research paper:

Topic: Large Language Models as autonomous agents — capabilities, limitations,
and emerging challenges in tool use and multi-step reasoning.

Include:
- A 3–4 paragraph narrative synthesis (not a list of summaries)
- At least 8 plausible in-text citations in APA format
- A "Research Gaps" subsection (3–4 sentences identifying open questions)
- A formatted reference list at the end

Target audience: Peer reviewers at an ACM or IEEE conference.
Save it as "literature-review-draft.md"
```

**What to observe:**

- Bob writes in academic register without switching to a casual tone
- Bob structures citations and the reference list in the correct format
- The output is a genuine starting point for a real literature review section

**Discussion points:**

- How would you verify Bob's citations before submitting?
- Where is this most useful — early-stage drafting, or polishing a draft you've written?
- How do you frame AI-assisted writing for your students in terms of academic integrity?

---

## Part 3: Participant-Driven Activity (20 minutes)

!!! note "Before starting Part 3"
    Click **New Task** in Bob to clear the context window from your track exercise. You're starting something new — a clean context gives Bob a fresh start.

!!! tip "Facilitator framing"
    In this workshop, participants are using Bob as an agentic AI system to build artifacts for them. If you want to connect this more directly to the event theme of "building your own agents," position this section as a lightweight agent-design exercise: participants can define a role, instructions, and output style that make Bob behave like *their* agent for a domain they care about.

Now it's your turn. Use what you just learned to ask Bob to build something that **interests you** — a sample, a proof-of-concept, or a fun mock-up in a domain you care about. It doesn't have to be real or production-ready; the goal is to see how far Bob can take an idea you find genuinely interesting.

### Instructions

- **5 minutes:** Pick a topic or idea you're curious about — something from your field, a hobby project, or a "what if" scenario. See the examples below for inspiration.
- **10 minutes:** Work with Bob to build a sample artifact around that idea.
- **5 minutes:** Review the result. Ask Bob to revise one thing. Note what surprised you — good or bad.

### The One Rule

The artifact should be something that excites or interests you personally — not a work deliverable. Think POC, sample, or demo.

### Prompt-Writing Tips

- Start with context: describe the idea and why it's interesting to you
- Specify the output format (markdown, HTML, JSON, Python, etc.)
- Include a fictional or sample audience so Bob can tune the tone
- Give Bob a file name to save to — it helps Bob know the scope
- If you want to make it feel like "your" agent, start by defining its role and working style (for example: "You are my policy analyst for higher education" or "Act as my startup product strategist")

### Example Starting Points by Role

**For developers:**
```
Create a sample [language] script/service that [something you've always wanted to prototype].
Include [tests / documentation / sample data]. Save in "[folder-name]"
```
*Example: "Build a sample Python script that tracks the score of my fantasy football league
using mock data. Include a README. Save in 'fantasy-tracker/'"*

**For PMs and execs:**
```
Write a fictional [PRD / competitive brief / roadmap / status summary] for
[an imaginary product you'd love to exist]. Audience: [sample team / mock exec board].
Save as "[filename].md"
```
*Example: "Write a one-page product brief for a fictional app that recommends hiking trails
based on your mood. Audience: a small startup team. Save as 'trail-mood-brief.md'"*

**For professors:**
```
Create a sample [syllabus section / assignment / rubric / discussion prompt / exam question set]
for a fictional or aspirational [course name] course. Level: [undergraduate / graduate].
Topic: [something in your field you find fascinating]. Save as "[filename].md"
```
*Example: "Design a sample week-3 module for a fictional course on the ethics of AI in healthcare,
for undergraduates. Include a discussion prompt and a short assignment. Save as 'ai-ethics-week3.md'"*

### Facilitator Discussion Prompts

Once participants have their artifacts, bring the room back together and ask:

- What idea did you pick, and why?
- How close was Bob's first draft to what you imagined?
- What did Bob get right without extra guidance?
- What would you still change, and why?
- Can you see yourself using Bob this way for real projects in the future?

---

## Part 4: Discussion and Q&A (10 minutes)

Invite 3–4 participants to share:

- What they asked Bob to build
- What surprised them about the output
- One thing Bob did that they did *not* expect
- Whether they'd use or adapt the result in real work

Then open for Q&A. Common questions to be ready for:

**"Is this safe to use at my company?"**
Bob runs locally inside VS Code. Your prompts and files stay on your machine unless your organization's policy specifies otherwise. Always check your company's AI usage guidelines before using any AI tool with proprietary information.

**"How do I know if the output is correct?"**
You don't — without reviewing it. Bob is a strong starting point, not a final product. Always apply your domain expertise to validate what Bob produces, especially for code, data analysis, and citations.

**"Can Bob connect to the internet or my company's systems?"**
Not by default. Bob works with local files and tools. Integrations with external systems require configuration.

**"What's the difference between Bob and ChatGPT?"**
Bob is an *agentic* AI — it uses tools to read files, write files, run searches, and execute multi-step tasks inside your development environment. ChatGPT is a conversational model that responds to messages but does not autonomously take action on your system.

---

## Key Takeaways

This workshop aligns with the Silicon Valley Leadership Group's Agentic AI Task Force focus on practical, responsible adoption. Bob demonstrates how agentic AI can increase individual and team productivity, while reinforcing the need for human review, clear usage boundaries, and organizational policies for security, privacy, and accountability.

### For Everyone

- **Agentic AI executes** — it doesn't just suggest, it creates tangible artifacts
- **Natural language is the interface** — no special syntax, no commands to memorize
- **First drafts are strong starting points** — always review, refine, and apply your expertise
- **Iteration is fast** — ask Bob to revise, extend, or explain anything it produces

### For Developers

- Bob accelerates the "first hour" of any new feature, service, or script
- Focus shifts from writing boilerplate to reviewing and refining architecture
- Bob handles the mechanical work; you handle the judgment calls

### For PMs and Executives

- Common artifacts — PRDs, briefs, user stories, dashboards — are minutes away, not hours
- Bob is a force multiplier for stakeholder communication and cross-functional alignment
- Human judgment on strategy, priorities, and customer insight remains irreplaceable

### For Professors and Educators

- Course design, assignments, rubrics, and literature scaffolding can be drafted rapidly
- Bob can handle the structural and formulaic elements so you focus on the intellectual content
- AI literacy discussions — including how and when to use tools like Bob — are themselves a teaching opportunity

---

## Best Practices

### Do's ✅

- **Give Bob context** — tell it who you are, what the artifact is for, and who the audience is
- **Specify the output format** — markdown, HTML, Python, JSON, table, email, etc.
- **Ask Bob to explain its choices** — it will tell you why it structured something a particular way
- **Iterate** — treat Bob's first response as a draft and ask for revisions

### Don'ts ❌

- **Don't skip review** — Bob can make mistakes; always apply your expertise before using the output
- **Don't include sensitive data** — avoid putting confidential, proprietary, or personal data in prompts
- **Don't over-specify** — you don't need to tell Bob every implementation detail; give it the goal and let it work
- **Don't treat it as a replacement** — Bob amplifies your expertise; it doesn't substitute for it

---

## Facilitator Guide

### Pre-Workshop Setup

- Verify all participants have Bob installed and working in VS Code before the session starts
- Test the warm-up dashboard prompt yourself in advance — confirm it works in your environment
- Have the track exercise prompts available in a shared document so participants can copy-paste rather than type
- Identify which participants are likely in each track (ask in advance if possible)
- Have 2–3 backup prompts ready for the participant-driven activity in case anyone is stuck

### Timing Tips

- The warm-up exercise (Part 1) is the most important segment — don't rush it and don't skip opening the result in a browser
- During track exercises, circulate and help anyone who is stuck on setup rather than content
- For the participant-driven activity, give a 5-minute warning so participants can wrap up before the group discussion
- The Q&A segment is flexible — expand it if energy is high, use it to do a second participant demo if energy is low

### Managing Mixed Ability

- Encourage developers who finish early to attempt the data science variant (Exercise A2), add tests to their API, or spend extra time shaping Part 3 into a role-based "my agent" workflow
- For participants who are less technical, steer them toward the dashboard exercise (B2) — it's visually impressive with minimal technical knowledge required
- Remind everyone that the strength of the *prompt* matters more than technical background

### Success Criteria

The workshop is successful if participants leave with:

- A concrete mental model of the difference between agentic AI and a chatbot
- At least one artifact they actually want to keep or adapt
- A clear sense of where to use Bob in their own work next week
