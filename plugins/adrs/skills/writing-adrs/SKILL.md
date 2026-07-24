---
name: writing-adrs
description: Guidelines for writing Architecture Decision Records (ADRs). Use when drafting or reviewing ADR content.
---

# Writing ADRs

Reference guide for authoring ADR documents.

## Template

Use the template at [templates/ADR.md](./templates/ADR.md). Copy it to the ADR directory and fill in each section.

## File Placement

- Pending ADRs: `adrs/1-pending/YYYY-MM-DD-short-name/ADR.md`
- Implemented ADRs: `adrs/2-implemented/YYYY-MM-DD-short-name/ADR.md`
- Supporting documents: place alongside `ADR.md` in the same directory

New ADRs always start in `1-pending/`. The ADR is put up as a pull request for team review. When the PR merges, the ADR is approved. The subsequent PR that implements the decision moves the ADR directory from `1-pending/` to `2-implemented/`.

## Writing Style

- **Direct** -- lead with the point, skip preamble
- **Specific** -- name concrete files, functions, endpoints, data shapes
- **No filler** -- every sentence must add information
- **Scalable** -- ADRs can range from short and trivial to many pages long for complex, multi-faceted projects. Scale the depth to match the problem.
- **Portable** -- never include user-specific environment details such as absolute paths containing home directories, machine-specific file locations, or a list of worktrees. Use repository-relative paths instead.

## Citations and References

**All factual claims must include references.** This is non-negotiable.

- Web sources: link URL + quote the relevant passage
- Source code: file path with line range at a specific commit SHA. Line numbers MUST be accompanied by a commit SHA -- line numbers are meaningless without one because they are relative to a specific commit. Run `git rev-parse HEAD` to get the current SHA. Example reference format: `path/to/file.ts:42 (abc1234)`. Every cited SHA MUST resolve on `main`; audit citations for main-branch reachability before requesting review.
- User statements: attribute clearly (e.g., "Per user input: ...")
- If a fact can be verified but has not been, verify it now, not at implementation time
- If a fact cannot be located, ask the user; do not fabricate
- If a load-bearing claim cannot be cited at all, delete the design that depended on it. Shipping an "assumption" flag is not an escape hatch.

This prevents hallucinations, misinformation, and outdated information from influencing decisions.

## Section Guidance

### Executive Summary
- 2-3 sentences maximum
- What is being decided and why it matters
- No implementation details here

### Background Context
- Problem statement: what is broken, missing, or what new functionality is desired
- Prior art: what exists today, what has been tried
- Constraints: technical, organizational, timeline
- Cite all external facts

### Approach Overview
- High-level description of the chosen approach
- Keep to a few bullet points

### Approach Details
- All consequential implementation details
- Code patterns, data models, API changes, configuration, dependencies
- Must be detailed enough for another agent to implement from this document alone
- Include code snippets, schema definitions, or interface sketches where they clarify intent
- Cite source code references for existing patterns being extended

### Implementation Roadmap
- Ordered sequence of discrete steps
- Render each step as its own `### Step N: [name]` subsection with a prose description, an `Acceptance criteria:` line, a `Status:` line, and a `Dependencies:` line. Do not use a markdown table.
- Each step should be independently verifiable
- Not a timeline -- just the sequence
- Include what each step produces or changes

### Architecture Documentation Updates
- Ship the drafted architecture prose as a supporting document (for example `N-architecture-doc-updates.md`) carrying the exact text that will land under `architecture/`. Do not describe the changes abstractly.
- Name each destination file in `architecture/` and identify the insertion point. Embed exact tables, snippets, and paragraphs; do not gesture at them.
- The drafted prose must satisfy the architecture-author agent's ground rules (including "reads as what exists after the ADR ships, never as what changed"). Do not restate those rules here.
- If no `architecture/` directory exists yet, note that it should be initialized with `/init-adrs`
- As the ADR iterates through review, revise this section to reflect only the current proposed approach. When the ADR is approved, this section should describe exactly the documentation changes needed for the final decision, with no residue from prior iterations.
- If the decision has no impact on architecture documentation, state that explicitly rather than leaving the section blank

### Alternatives Considered
- Each alternative that was seriously evaluated
- Why it was rejected (specific technical or practical reasons)
- Any conditions under which the alternative might be reconsidered
