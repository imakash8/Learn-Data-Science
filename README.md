# Learn Data Science

Notes and small experiments from my data science learning journey.

## Topics

- [Poetry](./poetry/README.md) — Python dependencies and virtual environments.
- Add a folder such as `docker/` when starting notes on another topic.

## Project setup

The `pyproject.toml` and `poetry.lock` files at the repository root define the
shared Python project and its dependencies. Run Poetry commands from this
directory; topic folders are for notes, not separate Python environments.

```powershell
poetry install
poetry run python --version
```

Add topic-specific notes to that topic's folder. Keep reusable code, exercises,
and experiments in appropriately named folders as the repository grows.
