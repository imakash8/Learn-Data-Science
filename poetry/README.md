# Notes: Learning Poetry for Production-Ready Data Science

## Overview

Poetry is a dependency and environment management tool that helps keep Python projects organized, reproducible, and easy to deploy in data science workflows.

---

## 1. Install Poetry

```bash
pip install poetry
poetry --version
```

If you want Poetry to use a specific Python interpreter:

```bash
poetry env use "C:\Users\imaka\AppData\Local\Programs\Python\Python312\python.exe"
```

To keep the virtual environment inside the project folder:

```bash
poetry config virtualenvs.in-project true
```

This stores the virtual environment in a local `.venv` folder within the project directory.

---

## 2. Create a New Project or Initialize an Existing One

### Create a new project

```bash
poetry new learn_ds
```

### Initialize an existing project

```bash
poetry init
```

### Install dependencies for a cloned repository

```bash
poetry install
```

### Update dependencies when the project changes

```bash
poetry update
```

---

## 3. Add and Remove Packages

### Add common data science libraries

```bash
poetry add pandas numpy matplotlib scikit-learn
```

### Remove a package

```bash
poetry remove pandas
```

---

## 4. Important Poetry Files

Poetry creates and manages a few core files:

- `pyproject.toml`: Project metadata and dependency requirements.
- `poetry.lock`: Locked versions of dependencies to ensure consistent installs across machines.
- `.venv`: The isolated virtual environment where the dependencies are installed. Make sure to put this file in gitignore

Poetry helps make environments reproducible and avoid version conflicts.

---

## 5. Run Scripts in the Poetry Environment

Use the environment created by Poetry:

```bash
poetry run python script.py
```

This ensures the script runs with the correct dependencies from the project environment.

---

## 6. Common Workflow

```bash
poetry new learn_ds
cd learn_ds
poetry add pandas numpy matplotlib scikit-learn
poetry run python main.py
```

---

## 7. Docker Example

```dockerfile
FROM python:3.11-slim

WORKDIR /app

COPY pyproject.toml poetry.lock ./

RUN pip install poetry
RUN poetry install --only main

COPY src ./src

CMD ["poetry", "run", "python", "src/customer_churn/main.py"]
```

This is useful when you want the project to run in a consistent, portable environment using Docker.

---

## Quick Summary

- Poetry manages dependencies and virtual environments.
- `pyproject.toml` defines project needs.
- `poetry.lock` locks exact versions.
- Use `poetry install` to set up a project.
- Use `poetry run` to execute scripts inside the project environment.


