# Lab 6B: Student Concierge App (SJSU Edition)

## Overview

This optional follow-on lab is intended for student or developer audiences who want a longer, more technical Bob exercise after the main mixed-audience workshop.

**Who this is for:** Anyone who wants to go deeper after the main workshop — especially students, developers, or educators who'd like to see Bob build a real, runnable application from scratch, step by step.

**Time needed:** 30–45 minutes

**What you'll build:** A locally-running "Student Concierge" web application tailored to San José State University — a conversational assistant that helps students find campus resources, answer common questions, and navigate SJSU life.

---

## What Is a Student Concierge App?

A Student Concierge is a lightweight web application that gives students a single place to ask questions about campus life and get instant, structured answers. Think of it as a friendly, knowledgeable RA available 24/7 in a browser tab.

For SJSU, the concierge will know about:

- Campus buildings and office locations
- Key academic deadlines and registration dates
- Financial aid, tutoring, and advising resources
- Campus dining, recreation, and student organizations
- Emergency and health services

You will use Bob to build the entire application — backend, frontend, and sample data — through a series of guided prompts.

---

## Before You Start: Prerequisites

You need the following installed on your laptop before running the app. If you are not sure whether something is installed, the check commands below will tell you.

=== "Mac"

    Open **Terminal** (press `⌘ Space`, type `Terminal`, press `Enter`).

    Check Node.js:
    ```bash
    node --version
    ```
    Check npm:
    ```bash
    npm --version
    ```
    If either command says "command not found", install Node.js from [https://nodejs.org](https://nodejs.org) — download the **LTS** version and run the installer.

    Check Python (optional, for the data variant):
    ```bash
    python3 --version
    ```

=== "Windows"

    Open **PowerShell** (press `Windows key`, type `PowerShell`, press `Enter`).

    Check Node.js:
    ```powershell
    node --version
    ```
    Check npm:
    ```powershell
    npm --version
    ```
    If either command says "not recognized", install Node.js from [https://nodejs.org](https://nodejs.org) — download the **LTS** version and run the installer. **Restart PowerShell after installing.**

    Check Python (optional, for the data variant):
    ```powershell
    python --version
    ```

Once Node.js is confirmed, open **VS Code** with Bob and you are ready to go.

---

## Step 1 — Ask Bob to Scaffold the Project (5 minutes)

Start a new Bob conversation and paste this prompt exactly:

```
Create a Student Concierge web application for San José State University (SJSU).

The app should be a Node.js Express server with a simple browser-based chat interface.

Requirements:
- A single-page HTML/CSS/JS front end served by Express
- A POST endpoint at /api/ask that accepts { "question": "..." } and returns { "answer": "..." }
- A knowledge base module (knowledgeBase.js) containing at least 15 SJSU-specific Q&A pairs covering:
    - Campus buildings (King Library, Engineering Building, Student Union, etc.)
    - Key academic office locations (Registrar, Financial Aid, Advising)
    - Important semester dates (registration, add/drop, finals)
    - Student resources (tutoring center, counseling services, career center)
    - Dining and recreation (dining commons, Spartan Recreation Center)
    - Emergency contacts (campus police, student health center)
- Simple keyword matching: if the user's question contains a keyword from the knowledge base, return that answer; otherwise return a helpful fallback message
- A clean, SJSU-themed UI using SJSU's colors (blue #0055A2 and gold #E5A823)
- A package.json with a "start" script

Save everything in a folder called "sjsu-concierge"
```

**What to observe while Bob works:**

- Bob creates the folder structure before writing any code
- Bob populates the knowledge base with real SJSU information
- Bob wires the front end to the back end automatically
- Bob writes a `package.json` so the app is immediately runnable

---

## Step 2 — Run the App (3 minutes)

Once Bob finishes, follow the instructions below to start the server.

=== "Mac"

    In VS Code, open the integrated terminal (`⌃ `` ` ```) and run:
    ```bash
    cd sjsu-concierge
    npm install
    npm start
    ```
    Then open your browser and go to:
    ```
    http://localhost:3000
    ```

=== "Windows"

    In VS Code, open the integrated terminal (`` Ctrl+` ``) and run:
    ```powershell
    cd sjsu-concierge
    npm install
    npm start
    ```
    Then open your browser and go to:
    ```
    http://localhost:3000
    ```

You should see the SJSU Student Concierge chat interface. Try typing:

- `Where is the library?`
- `When does registration open?`
- `How do I get financial aid?`
- `Where can I get tutoring?`

---

## Step 3 — Expand the Knowledge Base (5 minutes)

The app works, but the knowledge base only has the starter entries Bob created. Ask Bob to enrich it:

```
Expand the knowledgeBase.js file in sjsu-concierge to add 10 more Q&A entries covering:
- The SJSU mascot and sports teams (Spartans)
- The CS and Engineering department offices
- Parking and transit options (campus garage, VTA light rail stop)
- Popular study spots on campus
- The SJSU campus store location and hours
- Internship and career fair information
- Campus Wi-Fi instructions for students
- The student ID card office
- Mental health and wellness resources
- How to contact a professor or department

Keep the same data structure as the existing entries.
```

Stop and restart the server after Bob finishes:

=== "Mac"
    ```bash
    # Press Ctrl+C to stop, then:
    npm start
    ```

=== "Windows"
    ```powershell
    # Press Ctrl+C to stop, then:
    npm start
    ```

Test the new entries by typing questions about the topics Bob just added.

---

## Step 4 — Improve the UI (5 minutes)

The functional chat works. Now make it look more polished:

```
Improve the front-end UI of the sjsu-concierge app:
- Add the SJSU Spartans name as a subtitle under the main heading
- Show a welcome message when the page loads: "Hi! I'm your SJSU Student Concierge.
  Ask me anything about campus."
- Style user messages differently from concierge responses
  (user messages right-aligned in gold, concierge responses left-aligned in blue)
- Add a typing indicator (animated "..." dots) that appears while the server is responding
- Make the input field clear automatically after each message is sent
- Ensure the chat scrolls to the latest message automatically

Do not change the server-side code — only update the front-end HTML/CSS/JS.
```

Reload the browser tab (no server restart needed for front-end changes) to see the improved UI.

---

## Step 5 — Add a "Suggested Questions" Feature (5 minutes)

One of the most useful UX patterns for a concierge app is surfacing common questions so users know what to ask:

```
Add a "Suggested Questions" feature to the sjsu-concierge front end:
- Show 4 clickable suggestion chips below the chat window on first load:
  "Where is King Library?", "When is registration?",
  "Where can I get tutoring?", "How do I get financial aid?"
- When a chip is clicked, send that question automatically as if the user typed it
- Hide the suggestion chips after the first message is sent
- Style the chips to match the SJSU color scheme

Only modify front-end files.
```

Reload the browser to test the suggestion chips.

---

## Step 6 — Export a Conversation Summary (5 minutes)

A useful feature for any concierge app is letting users save what they learned:

```
Add a "Download Summary" button to the sjsu-concierge app that:
- Appears in the UI after at least 2 messages have been exchanged
- When clicked, generates a plain-text summary of the conversation
  (each exchange as "You: [question]" and "Concierge: [answer]")
- Downloads the summary as a .txt file named "sjsu-concierge-summary.txt"
- Requires no server-side changes — implement entirely in the browser

Only modify front-end files.
```

Test by having a short conversation then clicking "Download Summary."

---

## Step 7 — Stretch Goal: Smarter Matching (optional, 10 minutes)

The current keyword matching is basic. If you want to make the concierge meaningfully smarter, ask Bob to upgrade it:

```
Improve the question-matching logic in the sjsu-concierge server:
- Instead of simple keyword matching, score each knowledge base entry
  by counting how many words from the user's question appear in the
  entry's keywords list (case-insensitive)
- Return the entry with the highest score if it is above 0
- If two entries tie, return both answers separated by a newline
- If no entry scores above 0, return the existing fallback message
- Add a "confidence" field to the API response (0.0–1.0, based on score
  relative to the question word count) so the front end can optionally
  display it

Update the /api/ask endpoint in server.js only.
```

After Bob updates the server, restart it and test with more natural phrasing like:

- `How do I get help paying for school?`
- `I need a quiet place to study`
- `Is there a gym on campus?`

---

## What You've Built

By the end of these steps you have a fully functional, locally-running Student Concierge application:

| File | Purpose |
| :--- | :--- |
| `server.js` | Express server, `/api/ask` endpoint, question matching logic |
| `knowledgeBase.js` | SJSU Q&A knowledge base (25+ entries) |
| `public/index.html` | Chat UI with SJSU branding |
| `package.json` | Dependencies and start script |

The app runs entirely on your laptop — no cloud account, no API key, no internet connection required after install.

---

## Taking It Further

If you want to continue developing the app after the workshop, here are some ideas to bring back to Bob:

| Idea | Prompt hint |
| :--- | :--- |
| Persist conversation history in a local SQLite database | *"Add SQLite persistence to log all questions and answers"* |
| Load the knowledge base from a JSON or CSV file | *"Move the knowledge base to a sjsu-kb.json file and load it at startup"* |
| Add a fuzzy search library (Fuse.js) for better matching | *"Replace keyword matching with Fuse.js fuzzy search"* |
| Deploy to a free hosting tier (Render, Railway, Fly.io) | *"Add a Dockerfile and Render deployment config"* |
| Swap in a real LLM for answers via a local Ollama model | *"Route unanswered questions to a local Ollama llama3 model"* |

---

*Optional activity designed for SJSU — adaptable to any university campus by updating the knowledge base.*
