# Eval runs

One row per run of an `evals/<skill>/` fixture.

| Date | Skill | Model | Result | Notes |
|---|---|---|---|---|
| 2026-10-12 | setup | claude-sonnet (CLI alias `sonnet`, Claude Code 2.1.287) | pass, 7 of 7, and the second run changed nothing | Headless (`claude -p`, plugin from `--plugin-dir`), told to accept every recommended answer, so the confirm step was not exercised by a person. The one-test-file command (`npx vitest run <file>`) was inferred and the run said so. |
| 2026-10-12 | writing-for-agents | claude-sonnet (CLI alias `sonnet`, Claude Code 2.1.287) | pass, 9 of 9 | Three further findings, none asking the document to grow. |
