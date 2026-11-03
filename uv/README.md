# Notes: Learning UV for Production-Ready Data Science

## Overview

UV is a fast Python package and project management tool developed by Astral. It helps manage Python versions, virtual environments, dependencies, and project installations in data science workflows.

---

## 1. Install UV

### macOS / Linux

```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```

Check the installed version:

```bash
uv --version
```
---

## 2. Create a New Project or Initialize an Existing One

### Create a new project

```bash
uv init learn_ds
cd learn_ds
```

### Initialize an existing project

```bash
uv init
```

### Install dependencies from an existing project

```bash
uv sync
```

### Update dependencies

```bash
uv lock --upgrade
uv sync
```

---

## 3. Add and Remove Packages

### Add common data science libraries

```bash
uv add pandas numpy matplotlib scikit-learn
```

### Remove a package

```bash
uv remove pandas
```

### Add a development dependency

```bash
uv add --dev pytest jupyter
```

---

## 4. Important UV Files

UV creates and manages a few core files:

- `pyproject.toml`: Project metadata and dependency requirements.
- `uv.lock`: Locks exact dependency versions to ensure consistent installations across machines.
- `.venv`: The virtual environment where project dependencies are installed. Make sure to add it to `.gitignore`.

UV automatically creates and manages the virtual environment when needed.

---

## 5. Run Scripts in the UV Environment

Use UV to run Python scripts:

```bash
uv run python script.py
```

Run a Jupyter notebook or another installed tool:

```bash
uv run jupyter notebook
```

UV automatically makes sure the project environment is synchronized before running commands.

---

## 6. Python Version Management

Install a specific Python version:

```bash
uv python install 3.12
```

Set the Python version for your project:

```bash
uv python pin 3.12
```

Check available Python versions:

```bash
uv python list
```

---

## 7. Common Workflow

```bash
uv init learn_ds
cd learn_ds

uv add pandas numpy matplotlib scikit-learn

uv run python main.py
```

When sharing the project with someone else, they can install the locked dependencies using:

```bash
uv sync
```

---

## 8. Docker Example

```dockerfile
FROM python:3.12-slim

WORKDIR /app

RUN pip install uv

COPY pyproject.toml uv.lock ./

RUN uv sync --locked --no-dev

COPY . .

CMD ["uv", "run", "--no-sync", "python", "main.py"]
```

This uses UV to install project dependencies inside the Docker image and run the application in a consistent environment.

---

## Quick Summary

- UV manages Python dependencies, virtual environments, and Python versions.
- `pyproject.toml` defines project metadata and dependencies.
- `uv.lock` locks exact dependency versions.
- Use `uv sync` to install project dependencies.
- Use `uv add` and `uv remove` to manage packages.
- Use `uv run` to execute scripts inside the project environment.
- Use `uv python install` to install Python versions.