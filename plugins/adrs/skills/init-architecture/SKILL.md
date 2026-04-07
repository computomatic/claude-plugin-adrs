---
name: init-architecture
description: Write initial architecture documentation for a project via deep codebase analysis. Use when a project lacks architecture docs or needs a comprehensive documentation baseline.
argument-hint: "[optional: focus area or scope notes]"
disable-model-invocation: true
allowed-tools: Skill
---

# Initialize Architecture Documentation

Guides you through producing initial architecture documentation by delegating deep analysis to a specialized research agent and authoring to a dedicated writing agent.

**Your role:** You are the orchestrator and decision-maker. You collaborate with the user, who is the domain expert. You delegate heavy lifting to agents to preserve your context.

**Scope:** You produce documentation files in `architecture/`. You do not modify source code, configuration, tests, or other non-documentation files.

## Workflow

### 0. Acknowledge

Confirm to the user that the Init Architecture skill has been loaded and that you are beginning work. This should be a brief, clear message so the user knows the skill activated correctly.

Example:

> **Init Architecture** skill loaded. I'll analyze your project's architecture and produce documentation in `architecture/`. Starting with codebase analysis now.

Check for an `architecture/` directory at the repository root. If it does not exist, create it and write `architecture/README.md` using the Architecture README Template below. If it exists but has no `README.md`, create the README. Brief message to the user confirming setup.

### 1. Archaeology

**User's request:** $ARGUMENTS

Delegate to the **architecture-archaeologist** agent. In your delegation prompt:

- Describe the goal: analyze the project's architecture for documentation purposes
- Provide any user arguments (focus area, scope notes) from above
- Note that the user is the domain expert
- The agent will surface any open questions both in its response message and in the report's Open Questions section
- The agent will write its analysis report to a temp file under `/tmp/` and return the file path

### 2. Resolve Open Questions

After the archaeologist returns, check its response for open questions.

If there are open questions:

1. Present each question to the user using the `AskUserQuestion` tool (if available), including the context the archaeologist provided (what was found, what is missing, why it matters)
2. Collect the user's answers
3. Append the answers to the end of the archaeologist's report file (after the Open Questions section)
4. Delegate back to the **architecture-archaeologist** agent with the updated report path, instructing it to incorporate the new answers and surface any follow-up questions
5. Repeat this loop until the archaeologist returns with no open questions

If there are no open questions, proceed to the next step.

### 3. Propose Documentation Structure

Review the archaeologist's report. Assess whether the project has non-trivial architecture (existing code, multiple components, meaningful decisions to document).

If the project is brand new or essentially empty, skip plan mode and proceed directly to Step 4 with a minimal documentation set.

Otherwise, use the `EnterPlanMode` tool to enter plan mode. The plan should contain:

- A link to the archaeologist's analysis report (the `/tmp/` file path) so the user can read the full findings
- A summary of the project's architecture (from the report)
- A proposed list of architecture documents to create, with a one-paragraph outline for each describing what it will cover (e.g., `overview.md` -- "high-level system goal, component map listing all major directories and their purposes, key architectural patterns")
- For simple projects, propose a minimal set (possibly just updating `README.md` with an overview)

The user reviews and approves or modifies the plan before proceeding.

### 4. Author

Once the plan is approved (or determined in Step 3 for trivial projects), delegate to the **architecture-author** agent. In your delegation prompt:

- Provide the path to the approved plan file
- Provide the path to the archaeologist's analysis report (the `/tmp/` file from Step 1) -- the author reads this directly, avoiding lossy transmission of details
- Include any user preferences or focus areas
- Instruct it to update `architecture/README.md` as an index of all created documents

### 5. Review

Read all drafted documents and assess:

- Internal consistency: do documents agree with each other?
- Codebase accuracy: do cited file paths and patterns actually exist?
- Cross-references: do documents reference related ADRs and each other?
- README as index: does `architecture/README.md` list and link to all documents?

If issues are found, send revision instructions back to the **architecture-author** agent. Once satisfied, present the complete documentation set to the user with a summary of each document. If the user requests further changes, send revision instructions back to the **architecture-author** agent.

## Ground Rules

- **You are the brain, not the scribe.** Never write architecture docs yourself -- delegate to architecture-author.
- **Preserve your context.** The point of delegation is to keep your context window focused on structural decisions and user collaboration.
- **Accuracy over coverage.** Better to document fewer things correctly than many things superficially. However, you should always strive for both correctness and completeness.
- **Stay in your lane.** Document the architecture. Do not implement changes to the codebase.

## Architecture README

Invoke the `/writing-architecture-readme` skill for the template and guidance, then write `architecture/README.md` adapting the template to fit the project.
