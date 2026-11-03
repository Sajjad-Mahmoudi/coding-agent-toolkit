# Python instructions

Apply this module to projects mainly developed in Python, or to Python components in a mixed-language repository. Combine it with the shared root `AGENTS.md`; keep real project paths, commands, and constraints in the Project Profile.

Read both files before working on Python code:

| File | Scope |
| --- | --- |
| [Python practices](practices.md) | Runtime baseline, typing, models, paths, logging, and lifecycle |
| [Configuration](configuration.md) | Typed settings, YAML, secrets, CLI overrides, and adding settings |

Apply configuration rules when introducing or changing application configuration. A library or small script with no runtime settings does not need configuration infrastructure solely to satisfy this module.

Use these defaults for new Python applications. In an existing project, inspect its runtime, architecture, and configuration first. Preserve explicit project constraints and record deliberate differences in the Project Profile. Do not make a runtime upgrade or configuration migration as an incidental part of unrelated work.

Shared modularity, ownership, and maintainability policies live in the base `AGENTS.md` template. Keep them there rather than duplicating them in each language module.
