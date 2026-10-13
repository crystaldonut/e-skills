# setup

## What it does

Reads a repo, proposes its config, and after confirmation writes `docs/agents/skillset.md`: tracker, commands, thresholds, docs paths, stacks, subagent models and compliance triggers. It adds a short `## Agent skills` block to the repo's `CLAUDE.md` or `AGENTS.md` pointing at that file. It writes nothing else.

## When to reach for it

Run `/e-skills:setup` once in each repo that uses the set, before any other skill. Run it again to switch tracker or after the repo's test, lint or typecheck commands change. Small changes are quicker made by hand in the config file.

## It's working if

- Every command in the config exists in the repo (a script, a Makefile target) and the proposal named the file each came from.
- A value the repo does not state is `unset`, not guessed.
- `git status --short` afterwards shows the config and the instructions file only.
- A second run updates the existing block and file in place and adds no duplicate.
- `evals/setup/` produces its expected outcome.
