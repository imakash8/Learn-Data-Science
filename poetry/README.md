# Learning Poetry for Data Science

## Overview

[Poetry](https://python-poetry.org/) manages Python project dependencies,
virtual environments, and package metadata. It helps keep a project's
environment reproducible across machines.

In this repository, Poetry manages **one shared Python project**. Its
`pyproject.toml` and `poetry.lock` files are at the repository root
(`learn_ds/`). This `poetry/` folder is for notes about Poetry; it is not a
separate Python project. Run the commands below from the repository root unless
a section says otherwise.

---

## 1. Install and Check Poetry

Install Poetry using the method recommended for your operating system in the
[official installation guide](https://python-poetry.org/docs/#installation).
Then check that it is available:

```powershell
poetry --version
```

Poetry itself is a development tool; it does not need to be added to this
project's dependencies with `poetry add`.

---

## 2. Configure and Install This Project

To select a specific Python interpreter, pass its full path:

```powershell
poetry env use "C:\Path\To\Python\python.exe"
```

To store the virtual environment inside the repository, enable Poetry's
in-project setting before creating the environment:

```powershell
poetry config virtualenvs.in-project true
```

The environment will be created in the root `.venv/` folder, which is ignored
by Git. Install the dependencies declared by this project:

```powershell
poetry install
```

For an existing project such as this one, use `poetry install` rather than
`poetry new`. The `poetry new <name>` command is for creating a separate,
brand-new project.

If a project directory has been moved, its old virtual environment may still
contain references to the previous location. Recreate it from the repository
root instead of editing files inside `.venv/`:

```powershell
poetry env remove --all
poetry install
```

---

## 3. Add, Remove, and Update Dependencies

Add the libraries needed for data science:

```powershell
poetry add pandas numpy matplotlib scikit-learn
```

Poetry updates both `pyproject.toml` (the declared requirements) and
`poetry.lock` (the resolved versions). Commit both files so the environment can
be reproduced.

Remove a dependency when it is no longer needed:

```powershell
poetry remove pandas
```

Install the versions already recorded in the lockfile with `poetry install`.
To resolve and install newer versions within the project's version
requirements, run:

```powershell
poetry update
```

---

## 4. Understand the Project Files

- `pyproject.toml` — project metadata, Python requirements, and direct
  dependencies.
- `poetry.lock` — exact resolved versions of dependencies.
- `.venv/` — the local virtual environment; it should not be committed.
- `src/learn_ds/` — the importable Python package for this project.
- `poetry/` — these notes; other learning topics can have sibling folders
  such as `docker/`.

The project distribution is named `learn-ds`, while its Python import package
is `learn_ds`. Hyphens are allowed in distribution names but not in Python
import names.

---

## 5. Run Python in the Poetry Environment

Prefix commands with `poetry run` to execute them in this project's
environment:

```powershell
poetry run python --version
poetry run python path\to\script.py
```

You can also start a shell inside the environment:

```powershell
poetry shell
```

The shell command is optional; `poetry run` works without activating anything.

---

## 6. Common Workflow

From the repository root:

```powershell
poetry install
poetry add pandas numpy matplotlib scikit-learn
poetry run python path\to\your_script.py
```

Add Poetry-specific explanations and examples in this folder. Put notes about
other subjects in their own folders. The root environment is shared, so avoid
creating another `pyproject.toml` for every topic unless that topic needs a
truly independent project or dependency set.

---

## 7. Using Poetry with Docker

The following is a small illustrative Docker example for a Python script in
`src/learn_ds/main.py`. Run `docker build` from the repository root, where
`pyproject.toml`, `poetry.lock`, and `src/` are located.

```dockerfile
FROM python:3.12-slim

ENV POETRY_VIRTUALENVS_CREATE=false \
    PYTHONUNBUFFERED=1

WORKDIR /app

RUN pip install --no-cache-dir poetry

COPY pyproject.toml poetry.lock ./
RUN poetry install --only main --no-root

COPY src ./src

CMD ["python", "-m", "learn_ds.main"]
```

`--no-root` installs the project's dependencies without trying to install the
project package before its source has been copied into the image. This example
assumes the script is a module at `src/learn_ds/main.py`; update the `CMD` to
match the code you add. For a production image, also consider pinning the
Poetry version and using a multi-stage build.

---

## Quick Summary

- Keep the shared `pyproject.toml` and `poetry.lock` at the repository root.
- Use `poetry install` to install the locked dependencies.
- Use `poetry add` and `poetry remove` to manage dependencies.
- Use `poetry run` to run scripts with the project environment.
- Keep topic notes in topic folders; give a topic its own environment only
  when it needs an independent project.
