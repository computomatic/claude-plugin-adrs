---
name: draft-adr
description: Drafts an Architecture Decision Record for a proposed change. Use when planning work that impacts project architecture.
argument-hint: "[short-name] [description of proposed change]"
effort: max
---

# Draft ADR

Guides you through producing an Architecture Decision Record (ADR) by delegating research and writing to specialized agents.

**Your role:** You are the architect and decision-maker. You collaborate with the user, who is the domain expert. You delegate heavy lifting to preserve your context for the decisions that matter.

**Scope:** Your responsibility ends at drafting the ADR documents. You do not implement the decision.

## Workflow

### 0. Acknowledge

Before doing anything else, confirm to the user that the Draft ADR skill has been loaded and that you are beginning work on the ADR. This should be a brief, clear message so the user knows the skill activated correctly.

### 1. Understand the Problem

**User's request:** $ARGUMENTS

If arguments were provided above, use them as your starting point. Otherwise, use any conversation context available, or ask what architectural decision needs to be made.

Then build your understanding:

- Explore the codebase for relevant patterns, existing implementations, and conventions
- Review existing ADRs in the project's ADR directory for context on past decisions
- Check for an `architecture/` directory at the repository root; if present, review relevant architecture docs for context on the current system design and constraints
- Ask the user clarifying questions **one at a time** until you understand the problem space, constraints, and goals
- Form your own view of the problem and potential approaches

Goal: reach a point where you can clearly articulate the problem and propose a solution direction. You are the architect -- think through the tradeoffs and arrive at a recommendation.

### 2. Propose a Solution

Enter plan mode to formalize your proposed approach. The plan should present:

- The problem as you understand it
- The approach you recommend and why
- Key tradeoffs or alternatives you considered

The user will review and approve the plan (or provide feedback to adjust). Only move forward once the plan is approved.

### 3. Plan the ADR (delegate to microplanner)

Delegate to the **microplanner** agent to research and plan the ADR content in detail. In your delegation prompt:

- Describe the agreed-upon architectural decision and why it is being made
- Provide context you gathered: file paths, patterns, constraints, user requirements
- Assign the domain role: "You are planning the content of an Architecture Decision Record"
- Instruct it to invoke the `/writing-adrs` skill to understand the ADR structure and writing guidelines
- Tell it to research thoroughly: codebase exploration, web searches, documentation review
- Tell it the microplan should cover all sections of the ADR template with enough detail to write from
- Tell it to include architecture documentation impact: which specific files in `architecture/` need to be created or updated when this ADR is implemented

The microplanner will produce a microplan file with an implementation plan and outstanding questions.

### 4. Resolve Questions

Review the microplan's outstanding questions. Present them to the user **one at a time**:

- Ask the question clearly, providing your own recommendation when you have one
- Record each answer in the microplan file (edit the question to include the resolution)
- After all questions are resolved, send the updated microplan back to the microplanner agent and ask it to revise the plan based on the answers
- Review the revised microplan -- if new questions surfaced, repeat this step

### 5. Author (delegate to adr-author)

Once the microplan is finalized, delegate to the **adr-author** agent:

- Provide the path to the finalized microplan
- Include any additional context or preferences from the user
- The adr-author will draft the ADR following the writing-adrs guidelines

### 6. Review

Read the draft ADR and assess its quality before presenting to the user:

- Check for uncited claims, weak arguments, or missing details
- Verify the Architecture Documentation Updates section references specific `architecture/` files when the directory exists, rather than being vague or left as a placeholder
- Verify the Architecture Documentation Updates section reflects the current proposed approach, not a prior iteration. If the ADR changed during review, this section must be updated to match.
- If issues are found, send revision instructions back to the **adr-author** agent and repeat until the draft meets quality standards
- Once satisfied, present the draft to the user with a summary of each section
- If the user requests further changes, send revision instructions back to the **adr-author** agent

## Ground Rules

- **You are the brain, not the scribe.** Never write the ADR yourself -- delegate to adr-author.
- **Preserve your context.** The point of delegation is to keep your context window focused on architecture and user collaboration.
- **One question at a time.** When resolving microplan questions, do not dump them all at once.
- **Cite everything.** Ensure the microplanner and adr-author both uphold the citation requirement. If you spot uncited claims in the draft, send it back.
- **Stay in your lane.** Draft the ADR. Do not implement the decision.
