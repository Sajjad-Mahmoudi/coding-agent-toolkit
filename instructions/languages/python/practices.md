# Python practices

Use with the module's [entry point](README.md), [project structure](structure.md), and [configuration instructions](configuration.md).

## Language and tooling

- Target Python 3.14+ for new projects and use modern type hints. Respect an existing project's declared runtime unless a migration is part of the task.
- Prefer uv for dependency and environment management in new projects. Keep metadata, dependency groups, and lockfiles consistent with the [project structure](structure.md#project-files). Respect an existing project's package manager.
- Use Ruff for both linting and formatting. Record the project's exact commands and configuration in the Project Profile.

## Data modeling

- Prefer inline type hints for simple structures. Introduce a local type alias or dataclass only when the structure is complex enough to make inline types difficult to read or maintain. Promote types to shared APIs only when they are reused or form part of a cross-module contract.
- Prefer Pydantic models for structured validation and serialization, especially for data crossing module or trust boundaries. Follow the project's existing use of Pydantic.

| Data structure | Preferred representation |
| --- | --- |
| Public or cross-module data models and schemas | Pydantic models or Pydantic dataclasses |
| Internal, non-shared structures that need a named model | Standard-library `dataclasses` |

- Prefer built-in Pydantic methods and features when they meet the requirement, including `pydantic-settings` for configuration.

## Logging and errors

- Use the project's logger utilities for diagnostic output. Avoid ad-hoc `print()` outside CLI or other user-facing output.
- Raise specific project exceptions where defined. When wrapping an exception, preserve its cause with `raise ... from exc`.
- Never swallow exceptions silently. Handle them explicitly and add useful context when logging or propagating a failure.

## Paths and lifecycle

- Prefer `pathlib.Path` for all filesystem paths.
- Keep functions focused and testable. Inject collaborators or pass dependencies explicitly when this helps isolate behavior.
- Keep imports free of runtime side effects. Open network connections, load large models, and read mutable runtime state through explicit initialization or lifecycle code.

## Testing

- Run the full project test suite before implementing changes to establish a known-good baseline. Record existing failures; if the suite is missing or blocked, report that limitation.
- Prefer updating existing test modules. Create new modules only when unavoidable.
- Skip low-value or irrelevant test cases; focus on meaningful behavior, regressions, and important contracts.
- After changes, follow the shared template's focused verification and required completion checks.
