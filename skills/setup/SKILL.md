---
name: setup
description: "Configure this repo for the e-skills set. Writes docs/agents/skillset.md and a pointer in CLAUDE.md or AGENTS.md. Run once per repo, and again to change tracker or refresh commands."
disable-model-invocation: true
source:
  - mattpocock/skills@49dd158 skills/engineering/setup-matt-pocock-skills/SKILL.md
  - mattpocock/skills@49dd158 skills/engineering/setup-matt-pocock-skills/issue-tracker-github.md
  - mattpocock/skills@49dd158 skills/engineering/setup-matt-pocock-skills/issue-tracker-local.md
  - mattpocock/skills@49dd158 skills/engineering/setup-matt-pocock-skills/domain.md
---

# Setup

Write the **repo config**, `docs/agents/skillset.md`, that every other skill in this set reads its values from, and point the repo's agent instructions at it. Explore, propose, confirm, then write.

The config's shape is [`../../templates/skillset.md`](../../templates/skillset.md). Read it before step 1: its sections are the list of what to find.

## 1. Explore

Find each value in the repo itself. Record beside every value the file it came from.

- **Existing config**: `docs/agents/skillset.md`. When it exists this run is an update: its values are the starting draft, and exploration only fills gaps and flags values the repo now contradicts.
- **Instructions file**: `CLAUDE.md` and `AGENTS.md` at the repo root, and whether either already holds an `## Agent skills` block. A `CLAUDE.md` that only imports `AGENTS.md` counts as `AGENTS.md`.
- **Tracker**: `git remote -v`. A GitHub remote gives the slug. A `.scratch/` directory is a sign of a local-markdown tracker already in use.
- **Commands**: the scripts in `package.json`, `Makefile`, `justfile`, `Cargo.toml`, `pyproject.toml` and the CI workflows, which show what the repo itself treats as its gates. One row per area when the repo has several (workspaces, `apps/*`, `packages/*`, a second language).
- **Thresholds**: coverage settings in the test config and CI, function-size and nesting rules in the lint config.
- **Docs**: where requirements, design docs, plans, ADRs, a glossary and a learnings file live, and any template file beside them.
- **Stacks**: the pack names under this plugin's `stacks/` directory, matched against what the repo uses.

Done when every row of the template has a value with its evidence, or is marked `unset`.

## 2. Propose

Show the whole draft config with the evidence for each value, then the pointer block from step 4 and the file it will go in.

Ask only where exploration left a real branch, one question at a time, leading with the recommended answer so one word accepts it:

- **Tracker**, when there is no GitHub remote, or `.scratch/` exists beside one: GitHub or local markdown. Fill the section from the matching block in [`tracker.md`](tracker.md).
- **Instructions file**, when neither `CLAUDE.md` nor `AGENTS.md` exists: which to create.
- **A command with two candidates**, such as a fast and a full test script: which one is the gate.

A value exploration could not find stays `unset`. A skill that needs it later asks then.

Done when the user has seen every section and every question above has an answer.

## 3. Confirm

Apply the user's edits to the draft and show what changed. Done when the user says to write.

## 4. Write

Write the confirmed config to `docs/agents/skillset.md`.

Put this block in the instructions file found in step 1, replacing an existing `## Agent skills` block in place and leaving every other section as it was:

```markdown
## Agent skills

Repo config for the e-skills set: `docs/agents/skillset.md`.
Read it before running a test, lint or typecheck command, using the tracker, or spawning a subagent.
```

Done when `git status --short` lists `docs/agents/skillset.md` and the instructions file, and nothing else new.

## 5. Report

Name the two files written, list every value left `unset`, and say that the config is edited by hand from here: this skill runs again only to switch tracker or to refresh after the repo's commands change.
