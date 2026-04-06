---
name: init-adrs
description: Scaffold the adrs/ directory structure in the current project. Use when setting up ADRs for the first time.
effort: min
---

# Initialize ADRs

Scaffolds the `adrs/` folder structure in a project that hasn't used ADRs before.

## Workflow

### 1. Check for Existing Structure

Look for an `adrs/` directory at the repository root.

- **If it does not exist:** proceed to step 2.
- **If it exists and matches the expected structure** (`1-pending/`, `2-implemented/`, and `README.md` all present): report that the ADR directory is already initialized and stop.
- **If it exists but does not match:** describe the current structure to the user and ask whether they want to migrate existing content to the expected format or leave it as-is. If they choose to migrate, rename/move directories to match the expected structure. If they choose to leave it, stop.

### 2. Scaffold

Create the following files:

- `adrs/README.md` -- use the exact content from the README section below
- `adrs/1-pending/.gitkeep`
- `adrs/2-implemented/.gitkeep`

### 3. Confirm

Report the files that were created and suggest the user run `/draft-adr` to create their first ADR.

## README Content

Write this content verbatim to `adrs/README.md`:

```markdown
# Architecture Decision Records

This directory contains Architecture Decision Records (ADRs) -- documents that capture significant technical decisions along with their context and consequences.

## Folder Structure

```
adrs/
  1-pending/        ADRs awaiting approval
  2-implemented/    ADRs that have been approved and implemented
```

Each ADR lives in its own subdirectory named `YYYY-MM-DD-short-name/`. The main document is always `ADR.md`. Supporting materials (diagrams, data, references) go alongside it in the same directory.

## Lifecycle

1. **Draft** -- Create a new ADR with `/draft-adr` and place it in `1-pending/`
2. **Review** -- Open a pull request. The PR is the review forum: the team comments, asks questions, and requests changes there
3. **Approved** -- When the PR merges, the ADR is approved
4. **Implemented** -- The subsequent PR that implements the decision moves the ADR from `1-pending/` to `2-implemented/`

## Creating a New ADR

Run `/draft-adr [short-name] [description]` to start.
```
