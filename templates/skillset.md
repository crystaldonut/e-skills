# Skill set config

The e-skills skills read every repo-specific value from this file. A value marked `unset` is asked for when a skill first needs it, and recorded here once answered.

## Tracker

<one block from the setup skill's tracker.md>

## Commands

Run from the repo root unless the row's path says otherwise. `<file>` stands for the test file to run.

| Area | Path | Test | One test file | Lint | Typecheck |
|---|---|---|---|---|---|
| <area> | <path> | <command> | <command with <file>> | <command> | <command> |

## Thresholds

| Threshold | Value |
|---|---|
| Coverage of changed lines, percent | unset |
| Function length, lines | unset |
| Nesting depth | unset |
| PR size before a split is suggested, changed lines | 400 |

## Docs

| Kind | Path | Template |
|---|---|---|
| Requirements | unset | unset |
| Design docs | unset | unset |
| Plans | unset | unset |
| ADRs | unset | unset |
| Glossary | unset | |
| Learnings | unset | |

## Stacks

Enabled packs: none

## Models

The model a skill names when it spawns a subagent. Edit a row to override it for this repo.

| Subagent work | Model |
|---|---|
| Reading, searching, summarising | haiku |
| Everything else | sonnet |

## Compliance

Optional. A PR whose diff matches a trigger carries the note beside it.

| Trigger | Note |
|---|---|
| unset | |
