Every PR must include an appropriate semver bump in `plugins/adrs/.claude-plugin/plugin.json`, reassessed when additional commits are pushed (e.g., escalating from patch to minor if scope grows).

## Versioning guide

This plugin ships agent prompts, skill definitions, and templates. There is no runtime API or code contract, so semver applies to the *behavior and interface experienced by users and orchestrating agents*.

**Patch** (0.0.x): Changes that refine existing behavior without altering what the agents or skills do from a user's perspective. Examples: rewording instructions for clarity, fixing typos, tightening or loosening existing guidance, adding internal guardrails, adjusting prompt structure that does not change outputs in a user-visible way.

**Minor** (0.x.0): Changes that add new capabilities or meaningfully change what users or orchestrating agents can do. Examples: adding a new skill or agent, adding a new section to a template, introducing a new workflow step in an existing skill, changing file placement conventions, renaming or reorganizing the directory structure in a way that requires users to update references.

**Major** (x.0.0): Changes that break existing workflows or require users to change how they invoke or interact with the plugin. Examples: removing a skill or agent, renaming a skill (breaking `/skill-name` invocations), changing the ADR directory structure in a way that invalidates existing ADRs, removing or renaming template sections that external tooling or user workflows depend on.
