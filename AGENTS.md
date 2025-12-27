# Repository Guidelines

## Project Structure & Module Organization
- `codeclash/` holds the Python package: `agents/` (player implementations), `arenas/` (game backends + Dockerfiles), `tournaments/` (orchestration), `analysis/` (metrics/viz), `viewer/` (Flask UI), `utils/` (shared helpers).
- `configs/` stores tournament YAMLs (e.g., `configs/test/`, `configs/examples/`, `configs/main/`, `configs/ablations/`).
- `tests/` contains pytest suites for arenas and integration.
- `docs/` is the MkDocs site; `scripts/` has helper CLIs; `main.py` is the primary entry point.

## Build, Test, and Development Commands
- `uv sync --extra dev`: install dev dependencies.
- `uv run python main.py <config>`: run a tournament (example: `uv run python main.py configs/test/battlesnake.yaml`).
- `uv run pytest`: run tests; add `--cov=codeclash` for coverage or `-n auto` for parallel runs.
- `uv run ruff check .`: lint; `uv run ruff format .`: format.
- `uv run mkdocs serve`: preview docs; `uv run mkdocs build`: build static docs.
- `uv run python scripts/run_viewer.py`: launch the results viewer.

## Coding Style & Naming Conventions
- Python 3.11+, 4-space indentation, line length 120.
- Ruff enforces linting and formatting; formatting uses double quotes.
- Tests follow `test_*.py` naming under `tests/` (mirrors `codeclash/arenas/*`).
- Config files use descriptive names with arena + models + rounds/sims (e.g., `BattleSnake__claude-sonnet-4-5-20250929__o3__r5__s1000.yaml`).

## Testing Guidelines
- Framework: pytest (+ pytest-cov, pytest-xdist).
- Prefer targeted test runs when iterating: `uv run pytest tests/arenas/test_corewar.py`.
- Add tests for new arenas/agents or update existing ones alongside behavior changes.

## Commit & Pull Request Guidelines
- Git history favors short, imperative messages like “Add …”, “Update …”, “Fix …”; PR numbers sometimes appear in parentheses.
- Create a feature branch (e.g., `feature/my-change`), keep PRs focused, and update docs/tests as needed.
- Before opening a PR, run `uv run pytest && uv run ruff check .` and include a concise PR description with rationale and validation steps.

## Security & Configuration
- Copy `.env.example` to `.env` and set `GITHUB_TOKEN` plus any LLM API keys; never commit secrets.
- Docker is required for arena execution; verify local Docker availability before running tournaments.
