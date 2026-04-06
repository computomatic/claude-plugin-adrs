---
name: init-architecture
description: Write initial architecture documentation for the project. Performs deep codebase analysis and produces comprehensive living documentation in the architecture/ directory.
argument-hint: "[optional: focus area or scope notes]"
disable-model-invocation: true
allowed-tools: Skill
---

# Initialize Architecture Documentation

Guides you through producing initial architecture documentation by delegating deep analysis to a specialized research agent and authoring to a dedicated writing agent.

**Your role:** You are the orchestrator and decision-maker. You collaborate with the user, who is the domain expert. You delegate heavy lifting to agents to preserve your context.

**Scope:** Your responsibility is producing architecture documentation in `architecture/`. You do not modify the codebase.

## Workflow

### 0. Acknowledge

Confirm to the user that the Init Architecture skill has been loaded and that you are beginning work. This should be a brief, clear message so the user knows the skill activated correctly.

Check for an `architecture/` directory at the repository root. If it does not exist, create it and write `architecture/README.md` using the Architecture README Template below. If it exists but has no `README.md`, create the README. Brief message to the user confirming setup.

### 1. Archaeology

**User's request:** $ARGUMENTS

Delegate to the **architecture-archaeologist** agent. In your delegation prompt:

- Describe the goal: analyze the project's architecture for documentation purposes
- Provide any user arguments (focus area, scope notes) from above
- Note that the user is the domain expert and the agent should use `AskUserQuestion` for any ambiguity
- The agent will write its analysis report to a temp file under `/tmp/` and return the file path

### 2. Propose Documentation Structure

Review the archaeologist's report. Assess whether the project has non-trivial architecture (existing code, multiple components, meaningful decisions to document).

If the project is brand new or essentially empty, skip plan mode and proceed directly to Step 3 with a minimal documentation set.

Otherwise, use the `EnterPlanMode` tool to enter plan mode. The plan should contain:

- A link to the archaeologist's analysis report (the `/tmp/` file path) so the user can read the full findings
- A summary of the project's architecture (from the report)
- A proposed list of architecture documents to create, with a one-paragraph outline for each describing what it will cover (e.g., `overview.md` -- "high-level system goal, component map listing all major directories and their purposes, key architectural patterns")
- For simple projects, propose a minimal set (possibly just updating `README.md` with an overview)

The user reviews and approves or modifies the plan before proceeding.

### 3. Author

Once the plan is approved (or determined in Step 2 for trivial projects), delegate to the **architecture-author** agent. In your delegation prompt:

- Provide the path to the approved plan file
- Provide the path to the archaeologist's analysis report (the `/tmp/` file from Step 1) -- the author reads this directly, avoiding lossy transmission of details
- Include any user preferences or focus areas
- Instruct it to update `architecture/README.md` as an index of all created documents

### 4. Review

Read all drafted documents and assess:

- Internal consistency: do documents agree with each other?
- Codebase accuracy: do cited file paths and patterns actually exist?
- Cross-references: do documents reference related ADRs and each other?
- README as index: does `architecture/README.md` list and link to all documents?

If issues are found, send revision instructions back to the **architecture-author** agent. Once satisfied, present the complete documentation set to the user with a summary of each document. If the user requests further changes, send revision instructions back to the **architecture-author** agent.

## Ground Rules

- **You are the brain, not the scribe.** Never write architecture docs yourself -- delegate to architecture-author.
- **Preserve your context.** The point of delegation is to keep your context window focused on structural decisions and user collaboration.
- **Accuracy over coverage.** Better to document fewer things correctly than many things superficially. The user can always run the skill again to expand coverage.
- **Stay in your lane.** Document the architecture. Do not implement changes to the codebase.

## Architecture README

Invoke the `/writing-architecture-readme` skill for the template and guidance, then write `architecture/README.md` adapting the template to fit the project.
