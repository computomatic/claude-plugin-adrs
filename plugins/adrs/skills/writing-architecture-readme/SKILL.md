---
name: writing-architecture-readme
description: Guidelines and template for writing architecture README files. Defines the C4-inspired documentation hierarchy and README structure.
user-invocable: false
---

# Writing Architecture READMEs

Reference for writing and updating `architecture/README.md` files. This skill defines the documentation hierarchy and provides a standard template.

## Documentation Hierarchy

Architecture documentation follows a C4-inspired hierarchy of increasing detail:

1. **System context** (`overview.md`) -- how the system fits into the broader landscape, external actors, and high-level responsibilities
2. **Container level** (directories per deployable unit) -- each major deployable or independently running component gets its own subdirectory with a `README.md`
3. **Component level** (files within container directories) -- individual component documentation covering internal design, patterns, and coupling decisions
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
  {container-name}/                  # Container level
    README.md                        # Container overview
    {component-name}.md              # Component level docs
```

## README Template

The following is a template for a standard software project. Adapt it to fit the project -- not all sections will apply (e.g., documentation projects, polyglot monorepos, infrastructure repos may need a different structure).

~~~~~markdown
# Architecture Documentation

This directory contains living documentation of the current system state.

## System Context Documents

| Document | Description |
|----------|-------------|
| [overview.md](overview.md) | {High-level system goal, how the system fits among other systems, external actors, major components, key patterns} |

## Cross-Cutting Documents

| Document | Description |
|----------|-------------|
| [dependencies.md](dependencies.md) | {External libraries, vendoring strategy, rationale for key dependency choices} |
| [dev-environment.md](dev-environment.md) | {Why the dev environment is designed as it is: benefits, trade-offs, constraints} |
| [tests.md](tests.md) | {Testing strategy, test architecture, coverage philosophy, test boundaries} |
| [ci.md](ci.md) | {CI/CD architecture, pipeline design, deployment strategy} |

## Containers

Each major deployable unit has its own subdirectory containing a `README.md` overview and component-level documentation files.

| Container | Description |
|-----------|-------------|
| [{container-name}/]({container-name}/) | {Purpose, responsibilities, key interfaces} |

## Maintenance

Architecture docs are updated as part of ADR implementation, guided by each ADR's "Architecture Documentation Updates" section.

## Relationship to ADRs

ADRs capture point-in-time decisions and rationale; architecture docs describe the current state that results from those decisions.
~~~~~

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

### Container READMEs
Each container's README covers its purpose, responsibilities, boundaries, and key interfaces. It serves as the entry point for understanding that deployable unit.

### Component docs
Individual component documentation within a container directory. Covers internal design rationale, patterns used, coupling decisions, and anything a developer needs to understand before modifying the component.
