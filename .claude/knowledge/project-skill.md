# Project Skill

Standards and conventions for all code in this project. AI coding agents (e.g.
Claude Code) use this as their master rules file.

## Hard Rules

1. **uv only** — every `python`, `pip`, `pytest`, `ruff`, `mypy` invocation
   must be prefixed with `uv run`. No global pip installs.
2. **Type hints** on all public functions and methods. No `Any` unless
   unavoidable.
3. **≥80% test coverage** — `uv run pytest` must pass.
4. **No secrets** in source. Load from environment variables or a `.env` file.
   Never commit `.env`.
5. **Async by default** for I/O work. Use `asyncio` or an async framework.
6. **Ruff + mypy clean** before every commit:
   ```bash
   uv run ruff check . && uv run ruff format --check . && uv run mypy src tests
   ```
7. **Conventional Commits** — `feat:`, `fix:`, `docs:`, `chore:`, `refactor:`.
8. **No commented-out code** in commits. Delete it or add a TODO with a ticket
   reference.

## Soft Conventions

- Prefer standard library over dependencies where the stdlib module is adequate.
- Use `logging` (not `print`) for runtime output.
- Keep files under ~500 lines; split into modules when exceeded.
- Test files mirror source layout: `src/app/module.py` → `tests/app/test_module.py`.

## Related

- [Feature Development Playbook](../playbooks/feature-development.md)
- [Prompt Engineer Guide](../prompts/Prompt-Engineer.prompt.md)
- [Contributing](../../CONTRIBUTING.md)
