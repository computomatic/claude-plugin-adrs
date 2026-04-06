# claude-adrs

A Claude Code plugin marketplace providing Architecture Decision Record (ADR) tooling.

## What's included

The `adrs` plugin provides:

- **`/draft-adr` skill** -- orchestrates the full ADR drafting workflow: problem exploration, solution design, research delegation, and authoring
- **`writing-adrs` skill** -- reference guide for ADR writing style, structure, and citation requirements
- **`adr-author` agent** -- specialized subagent for writing and revising ADR documents with rigorous citation standards
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

Start drafting an ADR:

```
/adrs:draft-adr [short-name] [description of proposed change]
```

The skill will guide you through understanding the problem, proposing an approach, researching details, and producing a well-cited ADR document.

## ADR directory conventions

By default, the plugin expects:

- Drafts: `adrs/1-draft/YYYY-MM-DD-short-name/ADR.md`
- Implemented: `adrs/implemented/`

These paths can be adjusted in your project's CLAUDE.md.

## License

MIT
