# Repository Guidelines

## Project Structure & Module Organization
- `main.py` is a thin entry point; migrate reusable pipelines and utilities into `src/` as they mature.
- `notebooks/eda` holds exploratory analyses and `notebooks/experiments` tracks modeling runs (`YYYYMMDD_##_slug.ipynb`); keep the chronological naming scheme intact.
- `tests/` starts with `test_main.py`; expand alongside new modules and mirror package layout.
- `images/` stores plots referenced in READMEs or reports. Source Kaggle data lives outside the repo—mount or symlink it locally when needed.

## Build, Test, and Development Commands
- `python -m venv .venv && source .venv/bin/activate` to match the pinned Python 3.13 in `.python-version`.
- `pip install -e .` installs the core package; use `pip install -e .[dev]` to pull in tooling like `pytest`.
- `python main.py` is the quick smoke check after environment tweaks.
- `jupyter lab` (from the repo root with the venv kernel) is the preferred notebook entrypoint.

## Coding Style & Naming Conventions
- Follow Black-compatible formatting: 4-space indentation, snake_case modules/functions, PascalCase classes, UPPER_CASE constants.
- Add type hints and concise docstrings describing feature assumptions or competition quirks.
- Name notebooks `YYYYMMDD_##_topic.ipynb`; store helper scripts in `src/` and avoid committing `.ipynb_checkpoints/` artefacts.

## Testing Guidelines
- Pytest drives the suite; keep cases under `tests/` with filenames `test_*.py` and function-based tests.
- Use fixtures or light abstractions to stub Kaggle data loads so runs stay deterministic and CI-friendly.
- Run `pytest -q` locally (add `--maxfail=1` for faster feedback while iterating).

## Commit & Pull Request Guidelines
- Keep commit subjects short, present-tense, and descriptive (e.g., `Add sliding window baseline`); append date tags when relevant, mirroring existing history.
- Expand in the body with experiment references, validation metrics, and dataset snapshots.
- Pull requests should outline scope, commands executed, before/after metrics, linked issues or Kaggle submissions, plus visuals from `images/` when applicable.
- Confirm the branch is rebased, linted, and tests pass before requesting review.

## Data & Competition Hygiene
- Never commit raw Kaggle files or submission CSVs; rely on local storage or `.kaggle` config.
- Keep secrets in a gitignored `.env` and document required variables in README updates.
- Redact proprietary feature names before sharing notebooks or plots externally.
