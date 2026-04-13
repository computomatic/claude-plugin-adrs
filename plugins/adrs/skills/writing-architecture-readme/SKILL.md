---
name: writing-architecture-readme
description: Guidelines and template for writing architecture README files. Defines the documentation hierarchy and README structure. Use when creating or updating an architecture/README.md file.
user-invocable: false
---

# Writing Architecture READMEs

Reference for writing and updating `architecture/README.md` files. This skill defines the documentation hierarchy and provides a standard template.

## Content Principle

Architecture documentation exists to capture what the code cannot tell you: reasoning, trade-offs, constraints, and the context behind non-trivial decisions. Before writing any statement, ask: "Would someone reading the relevant source file already know this?" If yes, leave it out. Never restate config file contents, describe what files contain when that is obvious from reading them, or include running instructions (those belong in the project README). Every sentence in an architecture doc should explain *why*, not *what*. This often produces short documents. That is correct. A document with three paragraphs of genuine rationale is more valuable than one with ten paragraphs of code restatement.

## Documentation Hierarchy

Architecture documentation follows a hierarchy of increasing detail:

1. **System context** (`overview.md`) -- how the system fits into the broader landscape: external actors, neighboring systems, and high-level responsibilities
2. **Container level** (`{container-name}/{container-name}.md`) -- a *container* is a separately deployable or independently running unit (e.g., an API server, a web frontend, a background worker, a database). Each gets its own subdirectory with a self-named document, so supporting docs and component documentation can live alongside
3. **Component level** (`{container-name}/{component-name}/{component-name}.md`) -- a *component* is a major structural unit within a container (e.g., a module, package, or service layer) that encapsulates a coherent set of responsibilities. Each gets its own subdirectory so supporting documents can live alongside
4. **Code level** -- explicitly excluded from architecture docs. The code itself serves this purpose.

Not every project needs all levels. A single-container application may only have system context and cross-cutting documents. Scale the hierarchy to match the project's complexity.

## Directory Structure

```
architecture/
  README.md                          # Index and organizational guide
  overview.md                        # System context level
  dependencies.md                    # Cross-cutting: external dependencies
  dev-environment.md                 # Cross-cutting: dev environment rationale
  tests.md                           # Cross-cutting: testing strategy
  ci.md                              # Cross-cutting: CI/CD architecture
  {container-name}/                    # Container level
    {container-name}.md               # Container overview
    {topic}.md                        # Supporting docs for container
    {component-name}/                 # Component level
      {component-name}.md             # Component overview
      {topic}.md                      # Supporting docs for component
```

## README Template

The following is a template for a standard software project. Adapt it to fit the project -- not all sections will apply and alternative sections might be appropriate (e.g., documentation projects, polyglot monorepos, infrastructure repos may need a different structure).

~~~~~markdown
# Architecture Documentation

This directory contains living documentation of the current system state.

## Documentation Levels

Architecture documentation follows a hierarchy of increasing detail:

- **System context** (`overview.md`) -- how the system fits into the broader landscape: external actors, neighboring systems, and high-level responsibilities
- **Containers** (`{container-name}/{container-name}.md`) -- a container is a separately deployable or independently running unit (e.g., an API server, a web frontend, a background worker, a database). Each gets its own subdirectory for supporting docs and component documentation
- **Components** (`{container-name}/{component-name}/{component-name}.md`) -- a component is a major structural unit within a container (e.g., a module, package, or service layer) that encapsulates a coherent set of responsibilities. Each gets its own subdirectory for supporting docs
- **Code level** -- explicitly excluded from architecture docs; the code itself serves this purpose

## Contents

| Document | Description |
|----------|-------------|
| [overview.md](overview.md) | {High-level system goal, how the system fits among other systems, external actors, major components, key patterns} |
| [dependencies.md](dependencies.md) | {External libraries, vendoring strategy, rationale for key dependency choices} |
| [dev-environment.md](dev-environment.md) | {Why the dev environment is designed as it is: benefits, trade-offs, constraints} |
| [tests.md](tests.md) | {Testing strategy, test architecture, coverage philosophy, test boundaries} |
| [ci.md](ci.md) | {CI/CD architecture, pipeline design, deployment strategy} |
| [{container-name}/{container-name}.md]({container-name}/{container-name}.md) | {Purpose, responsibilities, key interfaces} |
| [{container-name}/{component-name}/{component-name}.md]({container-name}/{component-name}/{component-name}.md) | {Internal design, patterns, coupling decisions} |

## Maintenance

Architecture docs are updated as part of ADR implementation, guided by each ADR's "Architecture Documentation Updates" section.

## Relationship to ADRs

ADRs capture point-in-time decisions and rationale; architecture docs describe the current state that results from those decisions.

## Section Guidance

### overview.md
System context: the system's purpose, how it fits among other systems and services, external actors that interact with it, and the high-level component map.

### dependencies.md
External libraries and services the system depends on. Vendoring strategy, version pinning approach, and rationale for key dependency choices. Focus on the "why" behind selections, not just a list.

### dev-environment.md
Why the dev environment is designed as it is -- the benefits, trade-offs, and constraints that shaped it. This is NOT a setup guide or how-to (those belong in the project's root README). Focus on architectural rationale: why certain tools were chosen, why the workflow is structured a particular way, what trade-offs were accepted.

### tests.md
Testing strategy and philosophy: what levels of testing exist, where test boundaries are drawn, coverage expectations, and the rationale behind the testing architecture. Includes test infrastructure decisions and patterns.

### ci.md
CI/CD architecture: pipeline structure, deployment strategy, environment promotion, and the reasoning behind workflow design. Covers both the "what" and "why" of the CI/CD setup.

### Container docs
A container is a separately deployable or independently running unit (e.g., an API server, a web frontend, a background worker, a database). Each container gets its own subdirectory with a self-named document (`{container-name}/{container-name}.md`) covering its purpose, responsibilities, boundaries, and key interfaces. Supporting documents (`{container-name}/{topic}.md`) and component subdirectories live alongside.

### Component docs
A component is a major structural unit within a container (e.g., a module, package, or service layer) that encapsulates a coherent set of responsibilities. Each component gets its own subdirectory (`{container-name}/{component-name}/{component-name}.md`) with supporting documents (`{container-name}/{component-name}/{topic}.md`) alongside. Covers internal design rationale, patterns used, coupling decisions, and anything a developer needs to understand before modifying the component.
~~~~~
