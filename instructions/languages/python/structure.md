# Python project structure

Use with the module's [entry point](README.md), [coding practices](practices.md), and [configuration instructions](configuration.md).

Prefer a `src/` layout for new Python applications. Replace `<package>` with the application's importable package name. Adapt the layout to the project's responsibilities; create directories when they have a concrete purpose.

## Project files

| Location | Responsibility |
| --- | --- |
| `pyproject.toml` | Project metadata, supported Python versions, dependencies, development dependency groups, entry points, and tool configuration |
| `uv.lock` | Committed dependency resolution for projects managed with uv |
| `.python-version` | Development interpreter selection, consistent with `requires-python` |
| `src/<package>/` | Importable application code |
| `config/` | Runtime YAML and its committed example; see [configuration locations](configuration.md#locations) |
| `.env.example` | Safe placeholders and names for environment variables when a template is useful |
| `tests/` | Automated tests when present; follow the project's existing test organization |

Keep runtime dependencies and development tools in their appropriate `pyproject.toml` groups. Keep generated output outside the importable source package. Exclude virtual environments, caches, generated output, and local secret files from version control.

## Application package

Keep each area focused on its responsibility. For a small application, ordinary modules may be sufficient; add subpackages as the code grows.

| Location under `src/<package>/` | Responsibility | When to introduce it |
| --- | --- | --- |
| `__init__.py` | Package marker and deliberate public exports | Every regular package; keep imports safe |
| `__main__.py` | Delegate module execution to the CLI entry point | The application supports `python -m <package>` |
| `cli.py` | Parse arguments, call application behavior, and present CLI errors or exit codes | A command-line interface is needed |
| `configs/` | Typed settings, configuration sources, environment handling, and settings creation | Runtime configuration needs dedicated modules |
| `<feature>/` | A cohesive feature or domain area, including the behavior and types it owns | The feature is substantial enough to need a package |

Choose domain and infrastructure modules from the project's actual responsibilities. Keep types near their owner; promote them to shared modules only when reuse or a public contract justifies it. Follow the [data modeling rules](practices.md#data-modeling).

## Dependency boundaries

- Keep core application behavior independent of interface-specific parsing, output, and process exit handling. Entry points translate external inputs and call application behavior.
- Pass validated settings and other collaborators explicitly to the code that needs them.
- Keep shared types independent of their consumers. Resolve circular imports by correcting ownership and dependency direction.
- Configuration loading must not depend on feature execution. See the [settings package responsibilities](configuration.md#settings-package).
- Keep `__init__.py` files focused on deliberate, safe public exports.

## Entry points

For applications that expose a CLI, use one entry function for both the installed command and module execution. For an example package named `my_app`, the entry-point declaration is:

```toml
[project.scripts]
my-app = "my_app.cli:main"
```

Its `src/my_app/__main__.py` delegates to that function:

```python
from .cli import main

if __name__ == "__main__":
    main()
```

Configure the build backend to include the source package and install the project before using its console command. Record verified launch commands in the Project Profile.

## Initialization

Load and validate effective settings and initialize required dependencies through explicit application startup or lifecycle code. Keep settings loading, logging setup, network connections, and filesystem writes out of import-time code.
