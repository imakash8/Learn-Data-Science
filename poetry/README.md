# Poetry

Notes on using Poetry to manage the shared Python project in this repository.

## What Poetry does here

The project configuration lives at the repository root in `pyproject.toml`,
with exact dependency versions recorded in `poetry.lock`. This folder is for
Poetry-specific learning notes; it is not a separate Poetry project.

Run the following commands from the repository root:

```powershell
poetry install
poetry add pandas numpy matplotlib scikit-learn
poetry run python --version
```

To use a particular Python interpreter:

```powershell
poetry env use "C:\Path\To\Python\python.exe"
```

To keep the virtual environment in the repository, enable
`virtualenvs.in-project` in Poetry's configuration before installing. The
repository ignores `.venv/`, so the environment itself is not committed.

## Key files

- `pyproject.toml` — project metadata and dependency requirements.
- `poetry.lock` — locked dependency versions.
- `.venv/` — local environment created by Poetry; do not commit it.

When adding another topic, create a sibling folder such as `docker/` for its
notes. Keep this shared project configuration at the repository root unless a
topic genuinely needs an independent Python project.
