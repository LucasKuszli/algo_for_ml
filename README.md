# algo_for_ml
Source code for the assignments in the course Algorithms for Machine Learning and Inference
# uv Quick start

This repository uses **uv** to manage the Python environment and dependencies.

## Prerequisites

* Python project metadata in `pyproject.toml`
* `uv` installed on your machine

### Install uv

Follow Astral’s installation instructions, then confirm it works:

```bash
uv --version
```

(Install methods vary by OS; see uv docs.) ([Astral Docs][2])

---

## Get set up (first time)

From the repository root:

```bash
uv sync
```

This will (if needed) create a local virtual environment (typically `.venv/`) and install dependencies from `uv.lock` / `pyproject.toml`. ([Astral Docs][1])

### Activate the environment (optional)

You can either:

* **Use `uv run`** (recommended: no activation needed), or
* Activate `.venv` like a normal venv.

macOS/Linux:

```bash
source .venv/bin/activate
```

Windows (PowerShell):

```powershell
.venv\Scripts\activate
```

(Activation is optional because `uv run` will run commands in the project environment.) ([Astral Docs][1])

---

## Run things

### Run a command in the project environment (recommended)

```bash
uv run python -m your_module
uv run pytest
uv run python scripts/something.py
```

`uv run` ensures your environment matches the lockfile before executing. ([Astral Docs][1])

---

## Add / remove dependencies

### Add a dependency

```bash
uv add requests
```

### Add a dev dependency (example)

If you use dependency groups (common), you might do something like:

```bash
uv add --group dev pytest
```

### Remove a dependency

```bash
uv remove requests
```

These commands update `pyproject.toml` and the lockfile as needed. ([Astral Docs][3])

---

## Locking + reproducibility

### Update (regenerate) the lockfile

```bash
uv lock
```

### Sync environment to the lockfile

```bash
uv sync
```

### CI / strict mode (recommended)

In CI you often want to **fail** if the lockfile is out of date rather than silently updating it:

```bash
uv sync --locked
```

(Some workflows also use `uv run --locked` for the same reason.) ([Medium][4])

---

## Useful commands

```bash
uv tree        # view dependency tree
uv build       # build distribution artifacts (if this is a package)
```

([Astral Docs][3])

---

## What files should be committed?

Typical uv project structure includes:

* `pyproject.toml` (project metadata + dependency requirements)
* `uv.lock` (exact resolved versions for reproducibility)
* `.python-version` (optional, if you use it)
* **Don’t commit** `.venv/` (local environment)

([Astral Docs][1])

---

## Troubleshooting

* If installs look “off”, try a clean sync:

  ```bash
  uv sync
  ```
* If the lockfile conflicts with dependency edits, regenerate it:

  ```bash
  uv lock
  uv sync
  ```
* If you activated a venv manually and commands behave differently, prefer:

  ```bash
  uv run <command>
  ```


[1]: https://docs.astral.sh/uv/guides/projects/?utm_source=chatgpt.com "Working on projects | uv - Astral Docs"
[2]: https://docs.astral.sh/uv/reference/cli/?utm_source=chatgpt.com "Commands | uv - Astral Docs"
[3]: https://docs.astral.sh/uv/getting-started/features/?utm_source=chatgpt.com "Features | uv - Astral Docs"
[4]: https://medium.com/tr-labs-ml-engineering-blog/using-uv-for-python-development-part-1-making-your-python-dev-experience-much-faster-da4928704097?utm_source=chatgpt.com "Using uv for Python Development: Part 1 of 2— Making ..."
