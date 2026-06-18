# IBM Bob Workshop for IBM Product Managers
## Accelerate Your PM Work with Agentic AI

### Workshop Overview
This hands-on workshop demonstrates how IBM Bob, an agentic AI assistant, can transform your daily work as a Product Manager at IBM. Through practical exercises, you'll experience Bob's capabilities in requirements writing, competitive research, roadmap planning, stakeholder communication, and more. Learn how to leverage Bob to increase productivity, sharpen your strategy, and accelerate product delivery.

**Duration:** 60 minutes

**Target Audience:** IBM Product Managers, Product Owners, and Product Strategy professionals

**Prerequisites:** Basic familiarity with product management concepts and workflows

**Materials Needed:** Laptop with Bob access, VS Code with Bob extension

---

## What is Agentic AI?

### Traditional AI vs. Agentic AI

**Traditional AI Assistants:**

- Answer questions and provide information
- Draft copy or summaries on request
- Offer suggestions and recommendations
- Passive interaction model

**Agentic AI (IBM Bob):**

- **Autonomous action:** Takes initiative to complete multi-step tasks
- **Tool usage:** Reads, writes, and modifies files independently
- **Multi-step reasoning:** Breaks complex product problems into executable steps
- **Context awareness:** Understands your product, market, and stakeholder landscape
- **Iterative refinement:** Adapts based on results and feedback

**Key Differentiator:** Bob doesn't just suggest—Bob executes, creating tangible PM artifacts like PRDs, roadmaps, and competitive briefs.

---

## Workshop Structure

### 60-Minute Agenda

- **10 minutes** - Welcome, workshop framing, quick Bob demo, and what Bob is and how to work effectively with it
- **15 minutes** - Guided exercise: rapid PM artifact creation with Bob
- **20 minutes** - Participant-driven activity: create the PM deliverable you want Bob to build
- **10 minutes** - Discussion and Q&A
- **5 minutes** - Key takeaways and next steps

---

### Part 1: Guided Exercise - Rapid PM Artifact Creation (15 minutes)

This section demonstrates Bob's ability to produce polished PM deliverables quickly. The goal is to show how Bob can turn a clear product idea into a structured, usable artifact in minutes.

#### Exercise 1: Write a One-Page Product Requirements Document (PRD)

**Objective:** Experience Bob's ability to scaffold a complete PM artifact from a short brief.

**Scenario:** You're launching a new feature and need a lightweight PRD to align your engineering and design partners before the sprint kicks off.

**Task:**
```
Write a one-page PRD for the following feature:

Feature: A smart meeting summary tool integrated into IBM Slack
- Automatically summarizes IBM Meetings recordings into key decisions,
  action items, and open questions
- Sends a formatted Slack message to the meeting channel after the call ends
- Allows attendees to react to action items to acknowledge ownership

Include:
- Problem statement
- Target users and personas
- Goals and success metrics (KPIs)
- Scope (in scope / out of scope)
- Key user stories (3–5)
- Open questions and risks

Keep it concise — one page, executive-friendly.
Save it as "meeting-summary-prd.md"
```

**What to observe:**

- Bob structures the PRD with standard PM sections automatically
- Bob infers reasonable assumptions and success metrics from the brief
- Bob produces a document ready to share with engineering and design
- Time saved compared to writing the same PRD from scratch

**Discussion Points:**

- Which sections did Bob get right without extra prompting?
- What would you refine or add before sharing with stakeholders?
- How could this speed up your sprint planning or intake process?

---

### Part 2: Build Your Own PM Deliverable (20 minutes)

#### Exercise 2: Create a PM Artifact Relevant to Your Current Work

**Objective:** Use Bob to generate a real, useful PM deliverable tied to your current product area, then review and refine it.

**Time allocation:**

- 5 minutes: Choose your deliverable and craft your prompt
- 10 minutes: Bob creates the artifact
- 5 minutes: Review, refine, and discuss

**Instructions:**

Pick a PM artifact you actually need right now — or one that would save you the most time. Keep the scope tight enough to produce something you can review in 5 minutes.

**Example prompts for common PM deliverables:**

**For an interactive HTML dashboard from a spreadsheet:**
```
Create a sample spreadsheet (data.xlsx) with product feedback data across
multiple columns: Submission Date, Product Area, Severity, Status,
Reporter, and Description.

Then, build a self-contained interactive HTML file that:
- Loads and displays all rows as a sortable table
- Provides dropdown filter controls for Product Area, Severity, and Status
- Shows a live count of visible rows as filters are applied
- Highlights Critical severity rows in red and High severity rows in amber
- Includes a "Clear Filters" button to reset all dropdowns
- Requires no external libraries or CDN — fully self-contained

Save the file as "feedback-dashboard.html"

Then, give me the interactive URL that I can click on to run the html in my browser.
```

**For a sprint metrics summary from a Jira export:**
```
I have a CSV export from Jira (sprint-export.csv) with columns:
Issue Key, Summary, Assignee, Story Points, Status, Epic Link,
Sprint, Created Date, Resolved Date.

Analyze the data and produce a sprint retrospective summary as a
markdown document that includes:
- Total stories completed vs. committed (with % completion rate)
- Story point velocity for each team member
- Top 3 epics by stories delivered
- List of any carried-over stories with their age (days since created)
- One-paragraph narrative summary suitable for a VP-level update

Save the output as "sprint-retro-summary.md"
```

**For writing user stories:**
```
Write a set of user stories for the following capability:

Product: IBM Watson Assistant
Feature: Bulk import of intents via CSV file upload

Include:
- 5–7 user stories in "As a [persona], I want [goal], so that [benefit]" format
- Acceptance criteria for each story (3–5 bullet points)
- Story point estimates (S/M/L)
- Notes on any edge cases or dependencies

Format as a markdown table.
```

**For competitive analysis:**
```
Create a competitive feature comparison matrix for:

Our product: IBM Instana (observability platform)
Competitors: Datadog, Dynatrace, New Relic

Compare across these dimensions:
- AI/ML anomaly detection
- Infrastructure monitoring
- Application performance monitoring (APM)
- Pricing model
- IBM Cloud integration
- Strengths and weaknesses summary

Format as a markdown table with a brief narrative summary at the bottom.
```

**For a release notes draft:**
```
Write customer-facing release notes for a product update with
the following changes:

Product: IBM Cloudant
Version: 3.5.0

Changes:
- New: Automated backup scheduling with configurable retention policies
- Improved: Query performance for large datasets (up to 40% faster)
- Fixed: Resolved intermittent sync failures in multi-region deployments
- Deprecated: Legacy HTTP basic auth endpoint (removal in v4.0)

Tone: Professional but accessible. Audience: developers and architects.
Include a "What's New", "Improvements", "Bug Fixes", and "Deprecation Notice" section.
```

**For a product roadmap summary:**
```
Create a 3-quarter product roadmap overview for:

Product: IBM MQ (enterprise messaging)
Audience: Executive stakeholders (VP level)

Themes:
- Q1: Cloud-native deployment enhancements
- Q2: Developer experience improvements and new SDKs
- Q3: AI-assisted queue optimization and anomaly detection

For each quarter include:
- Theme headline
- 3–4 key initiatives (one sentence each)
- Primary value delivered to customers
- Key dependencies or risks

Format as a clean markdown document, suitable for a QBR slide deck.
```

**For a stakeholder communication:**
```
Write an internal announcement email for IBM Slack announcing:

- Product: IBM Planning Analytics
- News: General availability of the new Excel plug-in with real-time sync
- Audience: Internal IBM sales and consulting teams
- Key messages: What's new, who it's for, how to get access, where to learn more
- Tone: Enthusiastic but concise — under 200 words

Include a subject line.
```

**Prompting guidance:**

- Give Bob the product name, audience, and context
- Specify the format you want (markdown, table, email, etc.)
- Include tone guidance (executive, technical, customer-facing)
- Ask Bob to flag assumptions it made so you can correct them
- Request a version you can copy-paste directly into a doc or slide

**What to observe:**

- How quickly Bob produces a structured, usable artifact
- Whether the content reflects realistic product thinking
- How well Bob adapts tone and structure to the audience
- What you would still want to refine with your domain knowledge

**Reviewing your artifact:**

Once Bob creates your deliverable:

1. Read it as if you're the intended recipient
2. Identify one thing Bob got right without extra guidance
3. Identify one thing you'd change and ask Bob to revise it
4. Consider whether you could use or adapt this in real work this week

**Facilitator discussion prompts:**

- What did you ask Bob to create?
- How close was Bob's first draft to what you'd have written?
- What does this free you up to focus on instead?
- Where does human PM judgment still matter most?

---

### Part 3: Discussion and Q&A (10 minutes)

Invite participants to briefly share:

- What PM artifact they asked Bob to create
- What surprised them about the output
- Where they'd still apply their own expertise
- One workflow or task they'll try with Bob this week

Use this time to compare how Bob performed across different PM contexts — new features, existing products, enterprise vs. developer audiences.

---

## Key Takeaways for IBM PMs

### 1. **Productivity Multiplier**

- Reduce time-to-first-draft by 60–80% for common PM artifacts
- Eliminate repetitive formatting and boilerplate writing
- Focus on high-value strategy, customer discovery, and prioritization decisions
- Accelerate cross-functional alignment and stakeholder communication

### 2. **Consistency Across Teams**

- Produce PRDs, user stories, and roadmaps in a consistent format
- Reduce back-and-forth with engineering caused by unclear requirements
- Ensure every artifact includes the sections stakeholders expect
- Scale PM best practices across the team without additional coaching

### 3. **Strategic Thinking Support**

- Use Bob to quickly generate a first-draft competitive analysis to stress-test
- Get a structured framework for a problem you're approaching for the first time
- Synthesize research, notes, or interview transcripts into actionable insights
- Explore "what if" scenarios for roadmap trade-offs

### 4. **Faster Stakeholder Alignment**

- Produce exec-ready summaries and briefings in minutes
- Draft communication for launches, deprecations, and roadmap updates
- Prepare QBR materials, OKR summaries, and board-level updates faster
- More time for the conversations that require a human in the room

### 5. **Competitive Advantage for Your Products**

- Respond to market changes with faster, better-informed roadmap pivots
- Deliver higher-quality requirements that reduce rework in engineering
- Ship features with clearer success metrics from day one
- Demonstrate rigor and speed in product leadership reviews

---

## Bob's Core Capabilities for PMs

### Document Creation

- ✅ PRDs, user stories, and acceptance criteria
- ✅ Competitive analysis and feature matrices
- ✅ Release notes and changelog drafts
- ✅ Stakeholder emails, announcements, and briefings

### Research & Analysis

- ✅ Synthesize notes, transcripts, or research into structured summaries
- ✅ Identify patterns and themes across customer feedback
- ✅ Draft SWOT analyses and market positioning statements
- ✅ Compare options and trade-offs with structured frameworks

### Roadmap & Planning

- ✅ Roadmap narrative summaries for different audiences
- ✅ OKR drafts and key result definitions
- ✅ Sprint planning artifacts and backlog descriptions
- ✅ Dependency mapping and risk documentation

### Presentation Support

- ✅ Executive summary slides and QBR narratives
- ✅ Product demo scripts and talking points
- ✅ Sales enablement one-pagers
- ✅ Internal FAQ documents for new features

---

## Best Practices for Using Bob as a PM

### Do's ✅

**Provide Rich Context**

- Include the product name, target audience, and business goal
- Mention IBM-specific standards, brand tone, or compliance considerations
- Specify the output format (markdown, table, email, bullet points)
- Share the audience for the artifact (engineering, exec, customer)

**Iterate and Refine**

- Treat Bob's first draft as a strong starting point, not a final product
- Ask Bob to revise specific sections rather than starting over
- Request alternatives for critical positioning or messaging choices
- Use Bob's output to spark your own thinking and refinement

**Leverage Bob's Breadth**

- Use Bob for the parts of PM work that are time-consuming but formulaic
- Ask Bob to apply PM frameworks (Jobs to Be Done, RICE scoring, etc.)
- Have Bob draft the document so you can focus on the strategic decisions inside it
- Use Bob to prep for meetings by drafting agendas, pre-reads, or talking points

**Maintain Your PM Judgment**

- Review every artifact before sharing with stakeholders
- Validate assumptions Bob makes about your product or market
- Apply your customer and business context that Bob doesn't have
- Make prioritization and strategy calls yourself — Bob informs, you decide

### Don'ts ❌

**Don't Skip Review**

- Always read Bob's output before sending to stakeholders
- Verify that metrics, names, and product details are accurate
- Ensure the tone matches your audience and IBM's brand standards
- Check that scope and trade-offs reflect your actual product decisions

**Don't Share Confidential Information**

- Avoid including unreleased roadmap details in prompts without care
- Don't share client-specific data, deal information, or NDA-protected content
- Be cautious with competitive intelligence that is proprietary
- Follow IBM's data handling and AI usage policies

**Don't Over-Rely**

- Bob accelerates your work — it doesn't replace your product intuition
- Customer empathy and strategic judgment remain your core PM skills
- Bob doesn't know your stakeholders, org dynamics, or unwritten constraints
- Use Bob as a force multiplier, not a decision maker

**Don't Forget the Human Element**

- Product management is fundamentally about people — customers, engineers, execs
- The relationships, trust, and influence you build are yours alone
- Use the time Bob saves you to invest more in those human connections
- Great PMs use AI to do more of what only they can do

---

*Workshop created for IBM Bob — Empowering IBM Product Managers with Agentic AI*
*Version 1.0 — Designed for IBM Product Managers and Product Owners*
*Duration: 60 minutes*
*Last Updated: 2026*
