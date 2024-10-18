A fork of [pre-commit](https://pre-commit.com/) with experimental `workdir` setting support.

Using this fork, you can configure some hooks to run "as-if" the selected subfolders were in repository root.

E.g., with the following directory structure:

```
.
├── .git
├── backend
│   ├── pyproject.toml
│   └── uv.lock
├── frontend
│   ├── package.json
│   ├── pnpm-lock.yaml
│   ├── biome.jsonc
│   ├── src
│   ├── tsconfig.json
│   └── vite.config.js
└── .pre-commig-config.yaml
```

the following file will find backend-related and frontend-related files correctly:

```yaml
repos:
-   repo: https://github.com/astral-sh/uv-pre-commit
    rev: 0.4.24
    hooks:
    -   id: uv-lock
        workdir: backend

-   repo: https://github.com/biomejs/pre-commit
    rev: "v0.5.0"
    hooks:
    -   id: biome-check
        additional_dependencies: ["@biomejs/biome"]
        language_version: "20.18.0"
        workdir: frontend
```
