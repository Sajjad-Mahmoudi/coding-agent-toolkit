# Python configuration

Use with the module's [entry point](README.md) and [Python practices](practices.md).

## Locations

| Location in the target project | Responsibility |
| --- | --- |
| `<source-root>/<package>/configs/` | Typed settings models and the `pydantic-settings` loader |
| `config/settings.yaml` | Local, non-secret runtime settings |
| `config/settings.yaml.example` | Committed template for user-configurable settings |
| Environment variables or local `.env` files | Secrets and environment-specific overrides |

Resolve the source directory from the actual project layout, for example `src/my_app/configs/`, and record it in the Project Profile. Do not create literal placeholder directories. The source package's `configs/` holds Python code; the root `config/` holds configuration data.

## Settings package

Keep typed settings and their loading code in `<source-root>/<package>/configs/`. Separate these concerns as the application grows:

| Concern | Responsibility |
| --- | --- |
| Models | Typed settings groups and the composed `AppSettings` model |
| Sources | Loading configuration values and applying the documented source priority |
| Overrides and validation | Mapping explicitly supplied overrides and validating the effective result |
| Public interface | A clear settings-loading entry point and specific configuration errors for callers |

Use as few modules as the application's complexity warrants. Choose filenames from their responsibilities; do not require a factory class or a separate module for every concern.

- Construct settings during application startup and pass the validated object to consumers. Importing the package must not load YAML or `.env` files, create settings instances, or initialize logging.
- Resolve configuration files from an explicit, documented application root or configuration directory. Avoid assumptions about the caller's working directory or a fixed number of source-tree parents.

## Settings and source priority

- Use `pydantic-settings` to load and validate typed configuration. Keep settings models and loader code in the settings-code directory above.
- Make all non-secret application settings configurable through `config/settings.yaml` at the project root.

Load runtime settings in the following priority order. The first source that supplies a field wins:

| Priority (highest first) | Source |
| --- | --- |
| 1 | Explicitly supplied CLI flags |
| 2 | Environment variables |
| 3 | Local `.env` files |
| 4 | `config/settings.yaml` |
| 5 | Defaults in settings models |

- Configure the loader explicitly to enforce this order, including YAML below environment sources. Environment variables override `.env` values within the environment layer.
- Preserve the distinction between an omitted CLI flag and one explicitly supplied by the caller. Omitted flags must not accidentally replace configured values with parser defaults.
- Validate the effective settings after applying overrides. Record the loader entry point and source precedence in the Project Profile.
- Preserve existing public settings-loading entry points and their documented override and validation behavior unless changing that contract is part of the task.

## Local settings and secrets

- Create and maintain `config/settings.yaml.example` as the template for local settings.
- Keep passwords, API keys, and other secrets in environment variables or local `.env` files, never in YAML. Do not commit secret values.
- Use the single canonical filename `config/settings.yaml.example`; do not maintain a duplicate `settings.example.yaml`.
- Keep secrets out of examples, documentation, and logs. Exclude local `.env` files from Git; committed examples must contain only safe placeholders.

## Add a setting

- Define new settings as typed models in `<source-root>/<package>/configs/` and compose them on `AppSettings`.
- Mirror user-configurable, non-secret fields in `config/settings.yaml.example`.
- Document secret environment variable names without their values.
- Preserve source precedence and CLI override behavior. Use focused checks for effective values and relevant invalid-input cases.
- Update affected configuration documentation and the Project Profile when the public configuration contract changes.
