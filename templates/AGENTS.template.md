# Repository Guidelines

## Project Documentation Architecture

Use specification documents as the project's primary long-term reference for business analysis, functional
requirements, technical design, and architecture. Write for both human developers and AI coding agents, explaining
the application's purpose, behavior, and key design decisions without requiring readers to study the source code first.

Always maintain a main `SPECS.md` at the project root, covering the project overview, shared business rules, and
project-wide design decisions. When a substantial area needs more detail, create a `SPECS-<area>.md` file in its
relevant directory and link to it from the root specification. Use descriptive names, such as `SPECS-api.md`, and
organize these files around cohesive areas, such as an API layer, user interface, or data processing pipeline,
rather than individual source files.

Update the specifications alongside the application to reflect its current intended state. Document each topic
in one appropriate place, use links instead of repeating details, and keep shared rules and decisions consistent.

### Documentation Philosophy

Each specification should explain, within its scope:
- the purpose, responsibilities, and expected behavior of the application or area;
- important business rules and workflows;
- significant architectural and design decisions, with their rationale;
- constraints and trade-offs that shape the design.

Avoid:
- duplicating source code or restating obvious implementation details;
- maintaining inventories of source files, functions, or classes;
- recording short-lived implementation details that are likely to become outdated.

Favor concepts and rationale. Include technical details when they clarify behavior, interfaces, or lasting constraints.

### Source of Truth

Source code is authoritative for what is currently implemented. The root and area specifications describe the intended
behavior, business rules, and design within their respective scopes.

When the implementation and documentation differ, investigate the relevant requirements and design decisions:

- if the implementation reflects the intended behavior, update the affected specifications;
- if the implementation is wrong, correct it and revise the specifications only if they also need clarification;
- if the intended behavior is unclear or specifications conflict, resolve the ambiguity before making changes.

Do not assume existing behavior is correct simply because it is implemented, or change specifications merely to match
the code. Keep affected documents consistent when resolving a discrepancy.

### Maintenance

Update the relevant specifications as part of any change that affects:

- application behavior, business rules, or user workflows;
- APIs or interactions between application areas;
- data models, storage, or database architecture;
- application or deployment architecture;
- security, permissions, or authorization;
- meaningful performance characteristics;
- documented design decisions or constraints.

Keep area-specific details in the relevant area specifications. Update the root specification when the project overview,
shared rules, or project-wide decisions change, and check related documents for consistency.

Purely internal refactoring does not require documentation changes unless it affects documented behavior, interfaces,
constraints, or architecture.

When work is delegated, the coordinating agent remains responsible for reviewing the completed work and ensuring
the affected specifications reflect the integrated result.

### Update Strategy

When updating the root or area specifications:

- revise existing sections when they already cover the topic;
- keep related information together and replace outdated statements;
- link to existing explanations instead of repeating them;
- add sections when they provide a clearer home for distinct topics;
- move detailed coverage into a focused area specification when its scope justifies a separate document;
- update summaries, links, and cross-references whenever content is moved, renamed, or split.

Keep the documentation coherent, concise, and easy to navigate as the application evolves.

### Document Structure

Use a consistent structure across specifications, with headings and detail suited to each document's scope. The root
specification should present the project-wide view and link to area specifications. Area documents should define their
purpose and boundaries, then cover the requirements and design relevant to that scope.

Recommended sections, included where relevant:

- Overview & Scope
- Functional Requirements
- Non-Functional Requirements
- Architecture
- Database Structure
- Architecture & Design Decisions
- Testing Strategy
- Known Technical Debt
- Additional Documentation

Use this as a starting point. Omit sections that do not apply, and add or combine sections when that improves clarity.
Keep shared explanations in one place and link to them from other specifications.

### Section Expectations

Apply these expectations to each specification's scope, including only the sections that are relevant.

**Overview & Scope:** Explain the purpose, intended users, responsibilities, and boundaries of the application or area.
For an area specification, summarize how it fits into the wider application.

**Functional Requirements:** Describe observable behavior: features, business rules, workflows, permissions,
validation, data lifecycles, and functional constraints. Focus on expected outcomes and contracts.

**Non-Functional Requirements:** Describe quality expectations and constraints, such as performance, scalability,
reliability, security, accessibility, and maintainability. State measurable targets where they are known.

**Architecture:** Describe major components, responsibilities, boundaries, interactions, and data flow at a conceptual
level. Cover external integrations and deployment where relevant. Use simple Mermaid diagrams when they improve
understanding of structure, workflows, or data flow.

**Database Structure:** Describe the logical data model by business domain or subsystem, including key entities,
relationships, and important constraints. Include tables or indexes when they explain meaningful design choices;
leave exhaustive column definitions and schema details to the implementation.

**Architecture & Design Decisions:** Explain significant choices and their rationale, trade-offs, and constraints.
Describe relevant alternatives when they help readers understand why a decision was made.

**Testing Strategy:** Describe how important behavior and risks are validated. Keep automated testing effort
proportionate to the significance and risk of changes, adding persistent tests where they provide lasting value.
Low-impact changes may use targeted checks when permanent tests would add little value.

**Known Technical Debt:** Record intentionally deferred issues, their impact, and relevant constraints or reasons for
deferral. Keep entries concise and remove them once resolved.

**Additional Documentation:** Index relevant area specifications and supporting documents, with a brief description
of each document's purpose and when to consult it. Use the root specification as the main index; area specifications
should link to related material within their scope.

### Document Scope

Keep each specification focused on the current intended behavior and design within its scope. Retain historical
context only when it helps explain a decision, constraint, or dependency that still affects the application.

When functionality is removed, replaced, or moved, update the affected descriptions and references. Remove
superseded information that no longer helps readers understand the current system.

## Engineering Principles

- Understand the relevant requirements and existing code before editing; fit changes to the project's architecture.
- All implementations, especially in data processing, must use reproducible programmatic reasoning grounded in logic
  or systematic methods and must not rely solely on large language model analysis, unless the requester has explicitly
  discussed and approved that exception.
- Make focused, maintainable changes and preserve unrelated work.
- Keep responsibilities cohesive and dependency boundaries explicit. Introduce abstractions for demonstrated needs.
- Follow established language and framework conventions and respect documented public contracts.
- Handle failures explicitly, add useful error context, and avoid silently discarding errors.
- Keep dependencies and lifecycle behavior explicit; avoid unexpected initialization or import-time side effects.
- Use comments to explain non-obvious behavior, constraints, or decisions that the code alone does not make clear.

## Change Planning and Commits

- For large changes, always break the work into logical, independently implementable parts. Implement and commit each
  part separately.
- Commit messages must follow the format `type(scope): <message>`.

## Adapting This File

When this template is adopted for a repository, the coding agent should populate and maintain the Project Profile
below as part of normal project work. The user should not have to fill in facts that the repository already establishes.

- Inspect the relevant specifications, README, manifests, lockfiles, scripts, tool configuration, and CI workflows.
- Replace placeholders with verified project facts. Do not copy another project's paths, tools, or runtime versions.
- Record exact commands, working directories, and prerequisites from repository evidence; distinguish discovery from
  successful execution. Never execute unresolved placeholders.
- If a fact cannot be established, mark it unconfirmed. Ask for clarification only when the missing information matters
  to the task and cannot be resolved from the available evidence.
- Add, rename, combine, or remove profile subsections to fit the actual project. Remove fields that do not apply.
- Keep the profile current when layout, tooling, commands, interfaces, or conventions change, and summarize updates
  in the work report. Preserve the reusable policies above; put project-specific details in the profile or scoped files.
- Keep guidance concise and actionable. Link to specifications and configuration for detail instead of copying them.

## Project Profile (Agent-Maintained)

The fields below are template placeholders, not claims about the current repository. Populate them when adapting
this template for a project, following the process above.

### Purpose & Toolchain

- Project purpose and scope: `<PROJECT_PURPOSE_AND_SCOPE>`.
- Languages and supported runtime versions: `<LANGUAGES_AND_RUNTIME_VERSIONS>`.
- Frameworks and major libraries: `<FRAMEWORKS_AND_MAJOR_LIBRARIES>`.
- Package manager, manifests, and lockfiles: `<PACKAGE_MANAGER_AND_MANIFESTS>`.
- Supported platforms and required local services: `<PLATFORMS_AND_LOCAL_SERVICES>`.

### Setup & Commands

Record the supported shell, environment activation, local data setup, and other prerequisites: `<SETUP_REQUIREMENTS>`.
Replace the table entries with literal commands and their working directories. Remove inapplicable rows and add
project-specific tasks where needed. Check the repository's scripts and CI before recording a command.

| Task | Working directory | Command |
| --- | --- | --- |
| Install dependencies | `<DIRECTORY>` | `<INSTALL_COMMAND>` |
| Start local development | `<DIRECTORY>` | `<DEV_COMMAND>` |
| Build | `<DIRECTORY>` | `<BUILD_COMMAND>` |
| Format | `<DIRECTORY>` | `<FORMAT_COMMAND>` |
| Lint / static analysis | `<DIRECTORY>` | `<LINT_COMMAND>` |
| Type check | `<DIRECTORY>` | `<TYPECHECK_COMMAND>` |
| Focused tests | `<DIRECTORY>` | `<FOCUSED_TEST_COMMAND>` |
| Full test suite | `<DIRECTORY>` | `<TEST_COMMAND>` |
| Additional checks / evaluations | `<DIRECTORY>` | `<ADDITIONAL_CHECK_COMMAND>` |

### Repository Layout & Boundaries

Describe important directories and their responsibilities; do not maintain an inventory of individual source files.

- Source areas and responsibilities: `<DIRECTORIES_AND_RESPONSIBILITIES>`.
- Architectural layers and allowed dependency flow: `<ARCHITECTURE_BOUNDARIES>`.
- Generated or vendored paths and their source or regeneration process: `<GENERATED_PATHS_AND_SOURCES>`.
- Relevant specification entry points: `<ROOT_AND_AREA_SPECIFICATION_LINKS>`.

### Language & Framework Practices

Record non-obvious conventions for the languages and frameworks actually used, with links to existing configuration
where possible. Cover typing, errors, logging, state, concurrency, or lifecycle rules only where they are relevant.

- Language and framework rules: `<LANGUAGE_AND_FRAMEWORK_RULES_OR_LINKS>`.
- Compatibility, versioning, and deprecation requirements: `<COMPATIBILITY_REQUIREMENTS>`.

### Configuration & Interfaces

Follow the existing configuration mechanisms. Keep secret values out of this file, source control, and logs.

- Configuration sources, defaults, and precedence: `<CONFIGURATION_SOURCES_AND_PRECEDENCE>`.
- Required variable names and safe example files, without secret values: `<ENVIRONMENT_NAMES_AND_EXAMPLE_FILES>`.
- Applicable interfaces and entry points, such as UI, API, CLI, or library: `<INTERFACES_AND_ENTRY_POINTS>`.
- Interface contracts, validation, error handling, and access rules: `<INTERFACE_CONVENTIONS_OR_SPEC_LINKS>`.

### Dependencies & Project Constraints

Use the declared package manager and lockfiles. Keep required, optional, and development dependencies in their
appropriate groups, and avoid incidental upgrades or toolchain changes unrelated to the task.

- Dependency addition and upgrade rules: `<DEPENDENCY_POLICY>`.
- Project-specific constraints and protected areas: `<PROJECT_CHANGE_CONSTRAINTS>`.
- Migration, data compatibility, and release requirements: `<MIGRATION_AND_RELEASE_REQUIREMENTS>`.

### Testing & Completion

- Use the existing test structure. Add lasting tests for meaningful behavior, regressions, and important contracts;
  use targeted checks for low-impact changes when permanent tests would add little value.
- Start with focused checks and run the required broader checks for the affected scope. Broaden verification when
  shared behavior, failures, or unresolved risks justify it; avoid tests that merely mirror the implementation.
- Check the resulting behavior where relevant, review the final changes for unintended edits, and maintain the
  affected specifications under the documentation policies above.
- Report what changed, the checks actually run and their results, and any unresolved limitations.

Record the project's concrete completion requirements:

- Required checks and test environments: `<REQUIRED_CHECKS_AND_TEST_ENVIRONMENTS>`.
- Optional, expensive, or external checks and when to run them: `<OPTIONAL_CHECKS_AND_RUN_CONDITIONS>`.
- Additional commit, review, and pull request conventions: `<COMMIT_AND_REVIEW_CONVENTIONS>`. Keep these consistent
  with [Change Planning and Commits](#change-planning-and-commits).

### Scoped Instructions

Keep shared project guidance in the root file. Use nested `AGENTS.md` files for substantial areas with distinct
conventions when useful, applying them according to the coding agent's instruction-scoping rules. Keep local rules
focused on their area instead of copying the root guidance.

- Scoped instruction files and their purposes: `<SCOPED_INSTRUCTION_FILES_AND_PURPOSES>`.
