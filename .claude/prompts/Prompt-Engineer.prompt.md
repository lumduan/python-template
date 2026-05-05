# Prompt Engineer Guide

Instructions for writing effective prompts for AI coding agents working on this
project.

## Role definition

Start every prompt by declaring the agent's role and the context it operates in:

```
You are a senior Python engineer working on the python-template project. Your
goal is to produce correct, well-typed, well-tested code that passes the
project's quality gates.
```

## Context loading

Before asking the agent to write code, ensure it has:

1. Read `.claude/knowledge/project-skill.md` for project rules.
2. Read files it will modify or call (explicitly list the paths).
3. Read the relevant test file(s) so it understands expected behavior.

## Output format

When asking for code, specify the contract:

- **What to produce**: function, class, module, or test.
- **Input / output types**: expected signatures and return values.
- **Edge cases**: what should happen on empty input, missing keys, network
  failure, etc.
- **What NOT to do**: "don't add a CLI", "don't change the database schema".

## Refusal cases

Tell the agent when to push back:

- The request violates a Hard Rule in `project-skill.md`.
- The request is ambiguous and needs clarification.
- The request introduces a dependency without a clear justification.

## Example: good prompt

```
Read .claude/knowledge/project-skill.md, src/main.py, and tests/test_main.py.

Add a `health_check()` async function in src/main.py that returns `{"status":
"ok"}`. Write a matching test in tests/test_main.py. Do not add a web
framework — return the dict from the async function directly.

Quality gate: uv run ruff check . && uv run mypy src tests && uv run pytest
must pass.
```

## Example: bad prompt

```
add a health endpoint
```

Too vague — the agent will guess at framework, signature, tests, and location.
