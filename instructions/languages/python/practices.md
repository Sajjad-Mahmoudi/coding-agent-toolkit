# Python practices

Use with the module's [entry point](README.md) and [configuration instructions](configuration.md).

## Runtime and typing

- Target Python 3.13+ for new projects and use modern type hints such as `str | None`, `list[str]`, and `dict[str, Any]`. Respect an existing project's declared runtime unless a migration is part of the task.
- Do not add backward-compatibility code unless explicitly requested.

## Models and paths

- Use `dataclasses` for internal domain models and Pydantic models for validation and serialization at system boundaries. Follow the project's existing use of Pydantic.
- Prefer built-in Pydantic methods and features when they meet the requirement, including `pydantic-settings` for configuration.
- Prefer `pathlib.Path` for filesystem paths.

## Logging and lifecycle

- Use the project's logging utilities for diagnostic output. Reserve `print` for CLI or other user-facing output.
- Keep functions focused and testable. Inject collaborators or pass dependencies explicitly when this helps isolate behavior.
- Keep imports free of runtime side effects. Open network connections, load large models, and read mutable runtime state through explicit initialization or lifecycle code.
