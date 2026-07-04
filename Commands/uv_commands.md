# UV Complete Command Cheat Sheet

A comprehensive guide to the `uv` package manager.

---

# Table of Contents

1. Installation
2. Checking Version
3. Creating Projects
4. Virtual Environments
5. Python Versions
6. Installing Packages
7. Removing Packages
8. Updating Packages
9. Running Python
10. Running Scripts
11. Dependency Management
12. Requirements.txt
13. Lock Files
14. Syncing Environments
15. Build & Publish
16. Pip Compatibility
17. Useful Commands
18. Common Workflows

---

# 1. Installation

## Windows

```bash
powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"
```

or

```bash
pip install uv
```

---

## Linux/macOS

```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```

---

## Verify installation

```bash
uv --version
```

---

# 2. Check Version

```bash
uv --version
```

Update uv

```bash
uv self update
```

---

# 3. Creating a New Project

Create a project

```bash
uv init my_project
```

Current folder

```bash
uv init
```

---

# 4. Virtual Environments

Create venv

```bash
uv venv
```

Specify name

```bash
uv venv .venv
```

Specify Python

```bash
uv venv --python 3.12
```

Activate (Windows)

```bash
.venv\Scripts\activate
```

Activate (Linux/macOS)

```bash
source .venv/bin/activate
```

Delete environment

Simply delete the folder

```bash
rm -rf .venv
```

or Windows

```powershell
rmdir /s .venv
```

---

# 5. Python Versions

Install Python

```bash
uv python install 3.12
```

Install latest

```bash
uv python install
```

List installed

```bash
uv python list
```

Find Python

```bash
uv python find
```

Use a specific Python

```bash
uv python pin 3.12
```

---

# 6. Installing Packages

Install package

```bash
uv add numpy
```

Multiple packages

```bash
uv add numpy pandas matplotlib
```

Specific version

```bash
uv add "numpy==2.0.1"
```

Minimum version

```bash
uv add "fastapi>=0.110"
```

Maximum version

```bash
uv add "django<5"
```

Git package

```bash
uv add git+https://github.com/user/repo.git
```

Local package

```bash
uv add ./mypackage
```

Editable package

```bash
uv add --editable .
```

Development dependency

```bash
uv add --dev pytest
```

Optional dependency

```bash
uv add --optional docs mkdocs
```

Extras

```bash
uv add "fastapi[all]"
```

---

# 7. Removing Packages

```bash
uv remove numpy
```

Remove dev dependency

```bash
uv remove --dev pytest
```

---

# 8. Updating Packages

Update all

```bash
uv lock --upgrade
```

Update one package

```bash
uv lock --upgrade-package numpy
```

---

# 9. Running Python

Run script

```bash
uv run main.py
```

Run module

```bash
uv run -m module_name
```

Run command

```bash
uv run python
```

Run IPython

```bash
uv run ipython
```

Run Jupyter

```bash
uv run jupyter notebook
```

---

# 10. Running Scripts with Temporary Dependencies

```bash
uvx black .
```

or

```bash
uv tool run black .
```

Run ruff

```bash
uvx ruff check .
```

Run pytest

```bash
uvx pytest
```

---

# 11. Dependency Management

Install from pyproject.toml

```bash
uv sync
```

Install including dev dependencies

```bash
uv sync --dev
```

Only production

```bash
uv sync --no-dev
```

Recreate environment

```bash
uv sync --reinstall
```

---

# 12. Requirements.txt

Generate requirements.txt

```bash
uv export -o requirements.txt
```

Install requirements

```bash
uv add -r requirements.txt
```

Using pip compatibility

```bash
uv pip install -r requirements.txt
```

Freeze

```bash
uv pip freeze
```

---

# 13. Lock File

Create lock

```bash
uv lock
```

Upgrade lock

```bash
uv lock --upgrade
```

Upgrade one dependency

```bash
uv lock --upgrade-package requests
```

---

# 14. Sync Environment

Install exactly what's in lock

```bash
uv sync
```

Reinstall everything

```bash
uv sync --reinstall
```

---

# 15. Build & Publish

Build package

```bash
uv build
```

Publish

```bash
uv publish
```

Publish to TestPyPI

```bash
uv publish --repository testpypi
```

---

# 16. Pip Compatibility

Install

```bash
uv pip install numpy
```

Uninstall

```bash
uv pip uninstall numpy
```

Freeze

```bash
uv pip freeze
```

List

```bash
uv pip list
```

Show

```bash
uv pip show numpy
```

Check dependencies

```bash
uv pip check
```

---

# 17. Tool Management

Install CLI tool

```bash
uv tool install black
```

Run tool

```bash
uv tool run black .
```

Upgrade tool

```bash
uv tool upgrade black
```

List tools

```bash
uv tool list
```

Remove tool

```bash
uv tool uninstall black
```

---

# 18. Cache

Clean cache

```bash
uv cache clean
```

View cache

```bash
uv cache dir
```

Prune cache

```bash
uv cache prune
```

---

# 19. Useful Commands

Show help

```bash
uv --help
```

Help for add

```bash
uv add --help
```

Verbose

```bash
uv -v
```

Very verbose

```bash
uv -vv
```

---

# 20. Common Workflows

## Start New Project

```bash
uv init my_project
cd my_project
uv venv
uv sync
```

---

## Existing Python Project

```bash
uv init
uv add fastapi
uv add pandas
uv add numpy
uv sync
```

---

## Install from requirements.txt

```bash
uv add -r requirements.txt
```

or

```bash
uv pip install -r requirements.txt
```

---

## Export requirements.txt

```bash
uv export -o requirements.txt
```

---

## Add Dev Tools

```bash
uv add --dev pytest
uv add --dev black
uv add --dev ruff
```

---

## Run Application

```bash
uv run main.py
```

---

## Run Tests

```bash
uv run pytest
```

---

## Format Code

```bash
uvx black .
```

---

## Lint Code

```bash
uvx ruff check .
```

---

## Update Everything

```bash
uv lock --upgrade
uv sync
```

---

## Build Package

```bash
uv build
```

---

## Publish Package

```bash
uv publish
```

---

# Useful Tips

- `uv add` modifies `pyproject.toml` and updates `uv.lock`.
- `uv sync` installs exactly what's in `uv.lock`.
- `uv run` executes commands inside the project's virtual environment automatically.
- `uvx` (or `uv tool run`) runs tools without permanently installing them in your project.
- Prefer `uv add` for project dependencies instead of `uv pip install` to keep your project configuration reproducible.