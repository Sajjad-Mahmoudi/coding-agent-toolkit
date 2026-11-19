# Python configuration

Use with the module's [entry point](README.md) and [Python practices](practices.md).

## Locations

| Location in the target project | Responsibility |
| --- | --- |
| `<source-root>/<package>/config/` | Typed settings models and the `pydantic-settings` loader |
| `config/settings.yaml` | Local, non-secret runtime settings |
| `config/settings.yaml.example` | Committed template for user-configurable settings |
| Environment variables or local `.env` files | Secrets and environment-specific overrides |

Resolve the source directory from the actual project layout, for example `src/my_app/config/`, and record it in the Project Profile. Do not create literal placeholder directories. The source package's `config/` holds Python code; the root `config/` holds configuration data.

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
- If the project uses `SettingsFactory.create_settings_with_validation`, preserve its CLI override and validation behavior. Do not introduce a factory solely to reproduce this name.

## Local settings and secrets

- Create and maintain `config/settings.yaml.example` as the template for local settings.
- Keep passwords, API keys, and other secrets in environment variables or local `.env` files, never in YAML. Do not commit secret values.
- Use the single canonical filename `config/settings.yaml.example`; do not maintain a duplicate `settings.example.yaml`.
- Keep secrets out of examples, documentation, and logs. Exclude local `.env` files from Git; committed examples must contain only safe placeholders.

## Add a setting

- Define new settings as typed models in `<source-root>/<package>/config/` and compose them on `AppSettings`.
- Mirror user-configurable, non-secret fields in `config/settings.yaml.example`.
- Document secret environment variable names without their values.
- Preserve source precedence and CLI override behavior. Use focused checks for effective values and relevant invalid-input cases.
- Update affected configuration documentation and the Project Profile when the public configuration contract changes.
