# Repository Guidelines

## Project Structure & Module Organization
`specs/001-i-want-to` holds the authoritative spec, contracts, and onboarding notes; update it first whenever scope changes. Implement code under a mirrored tree: `src/agents`, `src/workflows`, `src/ui`, and collect runtime artefacts in `outputs/`. Tests live alongside the runtime stack in `tests/unit`, `tests/integration`, and `tests/contract` so students can jump from spec to validation quickly. Automation snippets or prompt templates belong in `.specify/scripts`, while `CLAUDE.md` tracks stack decisions for quick agent refreshers.

## Build, Test, and Development Commands
Target Python 3.11+ with UV. After cloning, run `uv sync` to install dependencies and keep lockfiles aligned across classrooms. Start the Chainlit preview with `uv run chainlit run src/main.py --watch`; it reloads agent changes automatically. Validate behaviour with `uv run pytest`, adding `--cov` when you need coverage data, and introduce new packages through `uv add <package>`.

## Coding Style & Naming Conventions
Stick to typed, async-friendly Python. Modules, functions, and variables use `snake_case`; classes stay `PascalCase`; constants are upper snake case. Every public function and agent class includes type hints and a focused docstring describing inputs and outputs. Favour awaitable workflows inside agents to match LangGraph execution. Store API keys and toggles in `.env`, read them through configuration helpers, and avoid hard-coded secrets.

## Testing Guidelines
Pytest remains the single runner. Write unit tests around prompt formatting and state transformations, contract tests that assert schemas against `specs/001-i-want-to/contracts/`, and integration tests that simulate a full chat session. Name files `test_<module>.py` and highlight edge cases such as missing clarifications or failed document writes. A new agent ships with at least one regression test plus a passing happy path.

## Commit & Pull Request Guidelines
Use short, imperative commit titles (e.g., `Add clarification agent contract`). Bundle related changes and squash noisy fixups before sharing. Pull requests reference the relevant spec section, summarise behaviour updates, list the tests run, and attach UI captures when the Chainlit experience changes. Tag reviewers by ownership (agents, workflows, UI) to speed feedback.

## Agent-Specific Tips
Read `CLAUDE.md` before development sprints to refresh recent decisions. Version control prompt tweaks alongside code and log significant behaviour shifts in `specs/001-i-want-to/tasks.md` so the teaching team can roll improvements into future cohorts.
