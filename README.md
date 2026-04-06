# claude-adrs

A Claude Code plugin marketplace providing Architecture Decision Record (ADR) tooling.

## What's included

The `adrs` plugin provides:

- **`/init-adrs` skill** -- scaffolds the `adrs/` and `architecture/` directory structure
- **`/draft-adr` skill** -- orchestrates the full ADR drafting workflow: problem exploration, solution design, research delegation, and authoring
- **`/init-architecture` skill** -- deep codebase analysis and initial architecture documentation authoring
- **`writing-adrs` skill** -- reference guide for ADR writing style, structure, and citation requirements
- **`adr-author` agent** -- specialized subagent for writing and revising ADR documents with rigorous citation standards
- **`architecture-archaeologist` agent** -- specialized agent for deep analysis of existing project architecture
- **`architecture-author` agent** -- specialized agent for writing and updating architecture documentation
- **ADR template** -- structured template covering executive summary, background, approach details, implementation roadmap, and alternatives

## Installation

Add this marketplace to Claude Code:

```
/plugin marketplace add computomatic/claude-adrs
```

Then install the plugin:

```
/plugin install adrs@claude-adrs
```

## Usage

Initialize the directory structure:

```
/adrs:init-adrs
```

Start drafting an ADR:

```
/adrs:draft-adr [short-name] [description of proposed change]
```

The skill will guide you through understanding the problem, proposing an approach, researching details, and producing a well-cited ADR document.

Write initial architecture documentation:

```
/adrs:init-architecture [optional: focus area or scope notes]
```

Performs deep codebase analysis to understand existing architecture, proposes a documentation structure, and produces comprehensive living documentation in `architecture/`.

## ADR directory conventions

- Pending: `adrs/1-pending/YYYY-MM-DD-short-name/ADR.md`
- Implemented: `adrs/2-implemented/YYYY-MM-DD-short-name/ADR.md`

## Architecture directory conventions

The `architecture/` directory contains living documentation of the current system state:

- `architecture/README.md` -- index and explanation of the directory
- Individual documents: `architecture/{topic}.md` (e.g., `overview.md`, `dependencies.md`, `ci.md`)

Architecture docs are updated as part of ADR implementation, guided by each ADR's "Architecture Documentation Updates" section. ADRs capture point-in-time decisions and rationale; architecture docs describe the current state that results from those decisions.
