# Learn Data Science

Notes and experiments from my data science learning journey.

## Topics

1. [Poetry](./poetry/README.md) — Python dependency and virtual environment management.
2. [UV](./uv/README.md) — Fast Python package and project management.
3. Git.

## Project Setup

The `pyproject.toml` and lock files contain project metadata and dependency information.

### Using Poetry

```powershell
poetry install
```

### Using UV

```powershell
uv sync
```

These commands install the project dependencies after cloning the repository.

**Note:** Use the package manager corresponding to the project's lock file (`poetry.lock` for Poetry or `uv.lock` for UV).