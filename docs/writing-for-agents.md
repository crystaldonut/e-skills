# writing-for-agents

## What it does

Holds the rules for writing anything an agent reads: a skill, a `CLAUDE.md` or `AGENTS.md`, a doc behind a pointer. It covers how to word a pointer, where each piece of a document sits, how a step ends, when to split a document, and what to prune. `SKILL-MECHANICS.md` adds the parts that apply only to skills.

## When to reach for it

The model loads it by itself when it creates or edits a skill or an instructions file. Every skill in this repo is written and maintained under it.

## It's working if

- A reviewed document comes back with each finding tied to a named rule (no-op, duplication, negation, a step with no completion criterion, a cache of the environment).
- A rewritten document is shorter and every step ends on a condition that can be checked.
- `evals/writing-for-agents/` produces its expected findings.
