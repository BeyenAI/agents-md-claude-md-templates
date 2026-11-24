# AGENTS.md — Python 3.12 + FastAPI + uv + Ruff + Pytest
<!-- Generated & linted with https://findaitier.com/agents-md-generator/ (Codex 32 KiB budget: ~1.7 KiB / 5.2%) -->

## Environment & Tooling
This project uses **`uv`** for dependency and virtual environment management. Always prefix Python commands with `uv run` (never invoke global `pip` or bare `python`).

## Executable Commands
- **Sync dependencies**: `uv sync --all-extras`
- **Run single test file (preferred)**: `uv run pytest tests/unit/test_<module>.py -q`
- **Run single test function**: `uv run pytest tests/unit/test_<module>.py -k "test_name" -q`
- **Lint & autofix**: `uv run ruff check --fix .`
- **Format check**: `uv run ruff format --check .`
- **Static typecheck**: `uv run mypy src/`

## Architecture & Code Rules
- `src/app/api/v1/` — FastAPI routers. Keep route handlers thin: parse request via Pydantic v2 models, call a service in `src/app/services/`, and return an explicit `response_model`.
- `src/app/services/` — Pure domain and business logic. Services receive an `AsyncSession` via dependency injection.
- `src/app/models/` — SQLAlchemy 2.0 typed declarative models (`Mapped[...]`, `mapped_column(...)`).
- `migrations/` — Alembic migrations. Never edit already-applied revisions.

## Non-Negotiable Constraints
- Use Pydantic v2 syntax (`model_validate`, `model_dump`, `ConfigDict`); never use deprecated v1 `.dict()` or `class Config:`.
- All I/O (database queries, HTTP calls via `httpx.AsyncClient`) must be `async`/`await`; never call blocking `requests` or `time.sleep` inside async endpoints.
- Before reporting a task complete, run `uv run ruff check .`, `uv run mypy src/`, and the relevant `uv run pytest` target.
