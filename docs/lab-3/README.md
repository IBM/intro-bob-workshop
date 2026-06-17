# IBM Bob Workshop for IBMers
## Accelerate Your Work with Agentic AI

### Workshop Overview
This hands-on workshop demonstrates how IBM Bob, an agentic AI assistant, can transform your daily work at IBM. Through practical exercises, you'll experience Bob's capabilities in code development, documentation, analysis, automation, and more. Learn how to leverage Bob to increase productivity, improve code quality, and accelerate project delivery.

**Duration:** 60 minutes

**Target Audience:** IBM employees (developers, architects, consultants, technical leaders)

**Prerequisites:** Basic familiarity with software development concepts

**Materials Needed:** Laptop with Bob access, VS Code with Bob extension

---

## What is Agentic AI?

### Traditional AI vs. Agentic AI

**Traditional AI Assistants:**

- Answer questions and provide information
- Generate code snippets on request
- Offer suggestions and recommendations
- Passive interaction model

**Agentic AI (IBM Bob):**

- **Autonomous action:** Takes initiative to complete tasks
- **Tool usage:** Reads, writes, and modifies files independently
- **Multi-step reasoning:** Breaks complex tasks into executable steps
- **Context awareness:** Understands project structure and relationships
- **Iterative refinement:** Adapts based on results and feedback

**Key Differentiator:** Bob doesn't just suggest—Bob executes, creating tangible deliverables.

---

## Workshop Structure

### 60-Minute Agenda

- **10 minutes** - Welcome, workshop framing, quick Bob demo, and what Bob is and how to work effectively with it
- **15 minutes** - Guided exercise: rapid prototyping with Bob
- **20 minutes** - Participant-driven activity: create the workshop you want Bob to build
- **10 minutes** - Discussion and Q&A

---

### Part 1: Guided Exercise - Rapid Prototyping (15 minutes)

This section demonstrates Bob's implementation capabilities in a compact, achievable exercise. The goal is to show how quickly Bob can turn a clear request into a useful starting point.

#### Exercise 1: Build a Small Product Catalog API

**Objective:** Experience Bob's ability to scaffold a useful, working solution quickly.

**Scenario:** You need a lightweight microservice prototype for a client or internal demo.

**Task:**
```
Create a small Node.js REST API for a product catalog service with:
- Express.js framework
- CRUD endpoints for products (GET, POST, PUT, DELETE)
- Basic input validation
- Error handling middleware
- Swagger UI for API documentation
- A simple README with setup instructions

Keep the implementation lightweight for a workshop demo.
Save it in a folder called "product-catalog-api"
```

**What to observe:**

- Bob creates multiple files with a sensible structure
- Bob turns a natural-language request into runnable code
- Bob includes supporting files such as setup instructions
- Time saved compared with building the same prototype manually

**Discussion Points:**

- What parts of the implementation were most useful?
- What would you still want to review or refine manually?
- How could this help with proof-of-concept work at IBM?

---

### Part 2: Build and Test Your Own Project (20 minutes)


#### Exercise 2: Create, Build, and Test a Quick Project

**Objective:** Use Bob to create a small, executable project relevant to your work, then test it to verify it works.

**Time allocation:**

- 5 minutes: Design and prompt Bob
- 10 minutes: Bob builds the project
- 5 minutes: Test and verify it works

**Instructions:**

Ask Bob to create a small, testable project that you can actually run and verify within the time limit. Keep it focused and achievable—think "proof of concept" not "production ready."

**Example prompts for quick, testable projects:**

**For Java developers:**
```
Create a simple Spring Boot REST API with:
- A single endpoint that accepts a product name and price
- Returns the price with 10% tax calculated
- Include a JUnit test that verifies the calculation
- Provide curl commands to test the endpoint
Keep it minimal—just one controller, one service method, and one test.
```

**For Python developers:**
```
Create a Python script that:
- Reads a CSV file with product data (name, price, quantity)
- Calculates total inventory value
- Exports results to a JSON file
- Include sample CSV data and a test function
- Provide commands to run and verify the output
```

**For Node.js developers:**
```
Create a Node.js Express API that:
- Has one POST endpoint accepting user data (name, email)
- Validates the email format
- Returns success or error response
- Include a simple test using curl or a test file
- Provide setup and test commands
```

**For DevOps/automation engineers:**
```
Create a bash script that:
- Checks if required services are running (e.g., docker, node)
- Reports their versions
- Creates a simple health check report
- Include test cases and expected output
- Make it executable and easy to verify
```

**For data engineers:**
```
Create a Python script that:
- Connects to a SQLite database (create sample DB)
- Performs a simple aggregation query
- Outputs results to console and CSV
- Include sample data insertion and query verification
- Provide commands to run and check results
```

**Prompting guidance:**

- Keep the scope small enough to build AND test in 20 minutes
- Focus on one specific, testable feature or function
- Include clear success criteria (what "working" looks like)
- Ask Bob to provide test commands or verification steps
- Request sample data or inputs if needed

**What to observe:**

- How quickly Bob creates a working, testable project
- Whether you can actually run and verify the output
- How well Bob includes testing/verification steps
- The quality and completeness of the minimal implementation

**Testing your project:**

Once Bob creates your project:

1. Follow Bob's setup instructions
2. Run the provided test commands
3. Verify the output matches expectations
4. Try one modification to see if you understand the code

**Facilitator discussion prompts:**

- What did you ask Bob to create?
- Were you able to run and test it successfully?
- What worked well? What would you change?
- How could you extend this for real work?

---

### Part 3: Discussion and Q&A (10 minutes)

Invite participants to briefly share:

- What they asked Bob to create
- What Bob produced
- What surprised them
- Whether they could use or adapt the result in real work

Use this time to compare how Bob responded across different roles such as developers, architects, consultants, and DevOps engineers.

---

## Key Takeaways for IBMers

### 1. **Productivity Multiplier**

- Reduce development time by 40-60% for common tasks
- Eliminate repetitive coding and documentation work
- Focus on high-value architecture and design decisions
- Accelerate client deliverables

### 2. **Quality & Consistency**

- Enforce coding standards automatically
- Generate comprehensive documentation consistently
- Implement best practices by default
- Reduce human error in repetitive tasks

### 3. **Knowledge Amplification**

- Access best practices across multiple technologies
- Learn new frameworks and patterns through examples
- Get instant code reviews and suggestions
- Bridge knowledge gaps in unfamiliar domains

### 4. **Client Value Delivery**

- Faster proof-of-concept development
- Higher quality deliverables
- More time for client interaction and requirements gathering
- Ability to handle more complex projects

### 5. **Competitive Advantage**

- Respond to RFPs faster with better proposals
- Demonstrate capabilities through rapid prototyping
- Deliver more value in the same timeframe
- Differentiate IBM's technical capabilities

---

## Bob's Core Capabilities Demonstrated

### File Operations

- ✅ Create complete project structures
- ✅ Read and analyze existing code
- ✅ Make surgical edits to specific files
- ✅ Organize multi-file projects

### Code Development

- ✅ Generate production-quality code
- ✅ Implement design patterns and best practices
- ✅ Add tests, documentation, and configurations
- ✅ Refactor and modernize legacy code

### Analysis & Insights

- ✅ Code review and quality assessment
- ✅ Security vulnerability identification
- ✅ Performance optimization recommendations
- ✅ Technical debt analysis

### Documentation

- ✅ API documentation generation
- ✅ Architecture diagrams and explanations
- ✅ User guides and tutorials
- ✅ Technical proposals and reports

### Automation

- ✅ CI/CD pipeline configuration
- ✅ Test automation and data generation
- ✅ Deployment scripts and procedures
- ✅ Monitoring and alerting setup

---

## Best Practices for Using Bob at IBM

### Do's ✅

**Be Specific and Contextual**

- Provide clear requirements and constraints
- Mention IBM-specific standards or client requirements
- Specify technology stack preferences
- Include security and compliance considerations

**Iterate and Refine**

- Start with core functionality, then enhance
- Ask Bob to explain architectural decisions
- Request alternatives for critical components
- Validate and test Bob's outputs

**Leverage Bob's Strengths**

- Use for rapid prototyping and scaffolding
- Automate repetitive documentation tasks
- Generate boilerplate and configuration files
- Perform code analysis and reviews

**Maintain Quality Standards**

- Review Bob's code before client delivery
- Ensure compliance with IBM and client standards
- Test thoroughly in appropriate environments
- Add human judgment for critical decisions

### Don'ts ❌

**Don't Skip Review**

- Always review code before production deployment
- Verify security implementations
- Test edge cases and error handling
- Validate against client requirements

**Don't Expose Sensitive Information**

- Avoid including client-specific data in prompts
- Don't share proprietary algorithms or IP
- Be cautious with security configurations
- Follow IBM's data handling policies

**Don't Over-Rely**

- Use Bob as a tool, not a replacement for expertise
- Apply critical thinking to Bob's suggestions
- Maintain your technical skills and knowledge
- Make architectural decisions with human judgment

**Don't Forget Context**

- Consider the full project lifecycle
- Think about maintenance and scalability
- Account for team skills and preferences
- Align with long-term technical strategy


---

*Workshop created for IBM Bob - Empowering IBMers with Agentic AI*
*Version 1.1 - Designed for IBM employees*
*Duration: 60 minutes*
*Last Updated: 2026*