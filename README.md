# Learn Data Science

Notes and experiments from my data science learning journey.

## Topics

1. [Poetry](./poetry/README.md) — Python dependency and virtual environment management (reference notes).
2. [UV](./uv/README.md) — Fast Python package and project management.
3. Git.

## Project Setup

This repository uses **UV** for Python dependency and virtual environment management.

The `pyproject.toml` file contains project metadata and dependencies, while `uv.lock` stores the exact dependency versions.

### Install Dependencies

After cloning the repository, run:

```bash
uv sync
```

### Run Python Scripts

```bash
uv run python main.py
```

### Add Dependencies

```bash
uv add pandas numpy matplotlib scikit-learn
```

**Note:** Poetry notes are retained for future reference, but UV is the active package manager for this repository.