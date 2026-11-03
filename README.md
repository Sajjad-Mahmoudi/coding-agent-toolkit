# coding-agent-toolkit

A reusable toolkit for AI coding agents: project instructions, setup prompts, and optional language guidance. Start with the shared `AGENTS.md` template and add only the modules your project needs.

## Choose the guidance

| Resource | Purpose | When to use it |
| --- | --- | --- |
| [AGENTS.md template](templates/AGENTS.template.md) | Shared engineering policies, specification documentation, and an agent-maintained Project Profile | Every project |
| [Initialisation prompt](prompts/initialisation.md) | Principal-engineer role and project scaffolding workflow | Starting or deliberately restructuring a project |
| [Python instructions](instructions/languages/python/README.md) | Python practices and typed runtime configuration | Projects mainly developed in Python, or their Python components |
| [Architecture and extension guide](docs/architecture.md) | Composition, directory responsibilities, and extension conventions | Adopting or extending this toolkit |

## Start a project

1. Copy `templates/AGENTS.template.md` to the project root as `AGENTS.md`. If one already exists, merge the relevant policies and preserve its project-specific instructions.
2. Use the [initialisation prompt](prompts/initialisation.md) to ask the agent to inspect the project, gather the minimum missing specifications, and establish its architecture and toolchain.
3. Ask the agent to populate and maintain the Project Profile from verified repository facts. Mark unconfirmed facts explicitly; the user should not need to supply information already in the repository.
4. Add the language modules the project needs. Keep shared policies in the base template and language-specific rules in their modules.

## Add Python guidance

Copy the complete `instructions/languages/python/` directory into your project as `.agent-toolkit/instructions/languages/python/`. Preserve its filenames so the internal links continue to work.

Add this instruction to the root `AGENTS.md` under **Language & Framework Practices**:

```markdown
For Python work, read `.agent-toolkit/instructions/languages/python/README.md`
and the instruction files it links to before editing. Apply these rules to
Python components; record verified project-specific choices in this profile.
```

The copy is local to the target project and does not require access to this repository during agent work. Linked Markdown is not automatically loaded by every coding agent, so the instruction explicitly tells the agent to read the module.

For a mixed-language repository, keep Python instructions scoped to Python components. Follow the coding agent's supported scoping rules if using a nested `AGENTS.md` instead.

## Extend the toolkit

Add each language under `instructions/languages/<language>/`, with a `README.md` entry point and focused files for substantial topics. Use `instructions/topics/<topic>/` for optional guidance shared across languages when such guidance is added. Keep workflow prompts, persistent instructions, copyable templates, and executable tooling separate.

See the [architecture and extension guide](docs/architecture.md) for extension conventions and the decisions made when organizing the Implementation page's guidance.
