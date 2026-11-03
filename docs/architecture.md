# Toolkit architecture and extension

The toolkit separates persistent project policies, workflow prompts, and optional instructions. A project adopts the shared base and selects only the modules relevant to its stack or task. Adoption uses explicit copies and references; no generator, package manager, or runtime loader is required.

## Directory responsibilities

| Location | Responsibility | Current entry point |
| --- | --- | --- |
| `templates/` | Copyable starting points that agents adapt to a target repository | [AGENTS.md template](../templates/AGENTS.template.md) |
| `prompts/` | Prompts submitted to start a workflow | [Initialisation](../prompts/initialisation.md) |
| `instructions/languages/<language>/` | Optional policies for one programming language | [Python](../instructions/languages/python/README.md) |
| `docs/` | Toolkit adoption, architecture, and extension documentation | This guide |

Keep the existing `templates/AGENTS.template.md` path stable. Its specification-documentation policies and agent-maintained Project Profile remain the shared foundation.

## Composition and adoption

1. Adopt the base template as the target project's root `AGENTS.md`. Merge with an existing file rather than replacing project guidance blindly.
2. Copy each selected module under `.agent-toolkit/instructions/`, retaining its path below `instructions/`. For Python, the result is `.agent-toolkit/instructions/languages/python/`.
3. Add an explicit instruction to the Project Profile to read the module entry point and its linked policy files. A Markdown link alone does not guarantee the coding agent will load a file.
4. Keep verified commands, real paths, supported versions, and deliberate departures from toolkit defaults in the Project Profile. Scope language modules to the components they govern.
5. When adopting a later toolkit revision, review and merge its changes with the local copy. Copies do not update automatically.

The [README](../README.md#add-python-guidance) provides a ready-to-copy Python adoption instruction. Use the agent's supported instruction-scoping mechanism if a nested `AGENTS.md` is more appropriate for a mixed-language project.

Reusable defaults guide new projects. An explicit target-project constraint or requested task takes precedence over those defaults; it is not a reason to make an unrelated migration. Resolve any conflict about intended behavior before changing the affected behavior.

## Organizing the Implementation guidance

| Page content | Canonical home | Organization decision |
| --- | --- | --- |
| Add root `AGENTS.md` | [Adoption steps](../README.md#start-a-project) and [initialisation usage](../prompts/initialisation.md) | Separate the human setup action from the first prompt |
| Principal-engineer role and capabilities | [Initialisation prompt](../prompts/initialisation.md#first-prompt) | Preserve the full role in the workflow prompt |
| Specifications, stack, architecture, Git branches, best practices, and ownership | [Initialisation prompt](../prompts/initialisation.md#first-prompt) | Establish `main` and `dev` for new repositories; preserve existing workflows unless changing them is requested |
| Maintainability, modularity, ownership, coupling, and comments | [Shared engineering principles](../templates/AGENTS.template.md#engineering-principles) | These rules apply across languages despite appearing under Python on the page |
| Python runtime, typing, models, paths, logging, and imports | [Python practices](../instructions/languages/python/practices.md) | Keep Python-specific rules out of the shared base |
| Typed settings, files, secrets, and CLI overrides | [Python configuration](../instructions/languages/python/configuration.md) | Separate configuration policy from everyday coding practices |

### Configuration clarifications

- Standardize on `config/settings.yaml.example` and maintain one template. The original page also used `settings.example.yaml`; the updated page and this toolkit use the canonical name consistently.
- Settings code belongs in the actual source package's `config/`; runtime YAML belongs in the project root's `config/`. These directories serve different purposes.
- List all runtime configuration sources and require projects to document their precedence. Preserve existing override behavior rather than silently assigning a new order.
- Treat `SettingsFactory.create_settings_with_validation` as an existing-project contract to preserve, not a class every new project must invent.

## Add languages and other tooling

- **Another language:** create `instructions/languages/<language>/README.md`. State when it applies and link focused files for substantial topics. Add it to the root resource table and include an adoption example. Keep shared policies in the base template.
- **Optional guidance across languages:** use `instructions/topics/<topic>/README.md` when the first such module is added, for example code review or release preparation. Universally applicable persistent policies belong in the base template instead.
- **Another workflow prompt:** add a focused file under `prompts/`, explaining when to use it and which instructions or inputs it needs.
- **Another copyable artifact:** add it under `templates/`. Keep the template separate from instructions explaining how to use it.
- **Executable tools or packaged agent skills:** introduce `tools/<tool>/` or `skills/<skill>/` only when there is an implementation. Document its entry point, prerequisites, supported agents or platforms, installation, and validation. Use the agent's supported native format for a packaged skill.

Create directories when they have content. Add a manifest or generator only when real adoption needs justify maintaining one.

## Review a toolkit change

- Preserve existing policies unless their change is intentional. Give each rule one canonical home.
- Check that scope and adoption instructions keep language-specific rules within the relevant components.
- Resolve inconsistent names and overlapping guidance explicitly. Keep the README resource table and relative links current.
- Check Markdown links, heading anchors, and code fences. Review the final diff for omissions or unrelated changes.
- For executable examples or tools, run checks appropriate to their behavior and record the results. Prose-only changes need focused documentation checks.
