# Repository Guidelines

## Project Structure & Module Organization

RoboMME is a Python benchmark for robot-memory manipulation. Runtime packages live in `src/robomme` and `src/robomme_plus`; task environments and metadata are kept there. Evaluation, replay, storage, and example entry points are in `scripts/` (including `scripts/plus_eval/`). Tests are organized under `tests/lightweight/` for fast logic checks and `tests/dataset/` for simulation and dataset behavior, with shared fixtures in `tests/_shared/`. Guides and data-format documentation are in `doc/`; images and logos are in `assets/`. Generated runs, videos, and local datasets should stay out of version control.

## Build, Test, and Development Commands

Use `uv` from the repository root:

```bash
uv sync                         # install the locked environment
uv pip install -e .             # install the package in editable mode
uv run scripts/run_example.py   # run the sample environment rollout
uv run python -m pytest tests/  # run the complete test suite
uv run python -m pytest tests/lightweight/  # fast logic tests
uv run python -m pytest -m dataset          # dataset-marked tests
```

Use `uv run scripts/dataset_replay.py --h5-data-dir <path>` to check downloaded HDF5 data. GPU, rendering, and dataset tests may require the dependencies and display setup described in `doc/`.

## Coding Style & Naming Conventions

Target Python 3.11+. Follow existing four-space indentation, PEP 8-compatible formatting, and clear `snake_case` names for modules, functions, and variables; use `PascalCase` for classes. Keep public behavior and documented data formats stable. Use `ruff` for formatting and linting when available (for example, `uv run ruff check .` and `uv run ruff format .`).

## Testing Guidelines

Tests use pytest. Name files `test_*.py` and test functions `test_*`. Mark expensive or environment-dependent cases with the registered `slow`, `gpu`, `dataset`, or `lightweight` markers. Reuse shared dataset fixtures so simulation data is generated once per session. Run focused tests while developing, then run the full suite before submitting changes.

## Commit & Pull Request Guidelines

Recent commits use short descriptions such as `add ood results` and `Clarify Plus submissions...`; keep commits focused and messages concise. Pull requests should explain the benchmark or documentation impact, identify affected paths, link any relevant issue or submission, and include test commands and results. For visual or evaluation changes, attach representative output or result files and note required hardware or datasets.

## Security & Configuration Tips

Do not commit downloaded datasets, credentials, private benchmark data, generated videos, or run artifacts. Keep local configuration and secrets in environment variables, and review generated files before staging them.
