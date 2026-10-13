# Plan

## Goal

Replace the hushmono quality-gate chain (`/test`, senior-qa-engineer, `/paranoid-review`, fullstack-code-reviewer, `/ceo-review`) with a smaller set that is stronger on review, adds build-side discipline, and can be installed in any repo as a plugin. Every skill is short, text-only, and names where it came from.

## What each source gets judged on

- **hushmono**: keep what has earned its place in daily use (base-branch detection, scope drift check, fix-first flow, PR gates record, SEC note, merged-PR preflight). Drop persona prose, cached commands, duplicated thresholds, and the two overlapping reviewer agents.
- **gstack (today)**: port review logic as plain text. Drop the runtime, telemetry, Codex integration, Greptile triage, update checks and generated preambles.
- **mattpocock**: port the build-side skills and the writing rules. Drop GitHub-only ticket flows, auto-commit, and the name collisions.

## Skill inventory

| Skill | Invoked by | Built from | Replaces in hushmono |
|---|---|---|---|
| `setup` | user | mattpocock setup, hushmono `.claude/docs/commands.md` | nothing (new) |
| `grill` | user | mattpocock grilling + domain-modeling (optional glossary/ADR) | plan mode habit |
| `spec` | user | mattpocock to-spec, hushmono requirements and design-doc templates | design-doc step |
| `tdd` | model | mattpocock tdd, tests.md, mocking.md; hushmono test conventions | TDD line in CLAUDE.md |
| `implement` | user | mattpocock implement, minus commit; hushmono dispatch model-routing rules | build step |
| `diagnose` | model | mattpocock diagnosing-bugs (feedback loop first); gstack investigate flake recipes | `/investigate` |
| `test` | user | hushmono `/test`, commands read from repo config | `/test` |
| `review` | user | hushmono paranoid-review core; gstack checklist and specialists; mattpocock spec axis; senior-qa and fullstack reviewer folded into specialists | `/paranoid-review`, senior-qa-engineer, fullstack-code-reviewer |
| `plan-review` | user | hushmono ceo-review + eng-review merged and pruned | `/ceo-review`, `/eng-review` |
| `pr` | user | hushmono `/pr`; mattpocock pr (evidence, merge danger) | `/pr` |
| `commit` | user | hushmono `/commit` | `/commit` |
| `retro` | user | mattpocock retro; gstack learn (learnings file) | nothing (new) |
| `handoff` | user | mattpocock handoff | nothing (new) |
| `guard` | user | hushmono guard (gstack lineage) | `/guard` |
| `writing-for-agents` | model | mattpocock, used to author and maintain this repo | nothing (meta) |

Dropped outright: `dispatch` as a skill (its routing table moves into the repo config and `implement`), `model-portfolio`, `dependency-management` and `troubleshoot` with its troubleshooter agent (hushmono-specific, stay there), `careful` (superseded by guard).

## Design notes per skill

### review

The centerpiece. Pipeline, each step one short section:

0. Detect base branch and fetch it. Diff is `origin/<base>...HEAD` plus the working tree.
1. Scope check. State the intent from the ticket, design doc or commits. Report CLEAN, DRIFT or REQUIREMENTS MISSING. Informational.
2. Critical pass, inline in the main agent: data safety (SQL plus whatever the enabled stack packs add, such as Firestore transactions and BigQuery cost), concurrency, LLM output trust boundary, enum and value completeness (read every consumer, not grep), gate integrity (a test removed, skipped or loosened, a timeout raised, an exception swallowed, a snapshot changed without its test; always ASK, never auto-fix), forced CRITICAL (data loss, trust-boundary bypass, uncapped spend; nothing downgrades these).
3. Sideways. For every finding, grep the same pattern at every other entry point: routes, workers, cron, webhooks, CLI. The worst sibling sets the severity. Siblings list under one finding as one decision.
4. Specialists as parallel Sonnet subagents, each prompt under 60 lines: security, testing, data and migrations, api contract, maintainability, frontend (only when the diff touches UI). The testing specialist absorbs senior-qa: it writes only tests, it writes a failing test for every bug it finds, it flags `.only` and `.skip`, and it reads thresholds from the repo config. The maintainability specialist absorbs fullstack-reviewer: function size and nesting limits come from the repo config, not from the prompt.
5. Merge. Dedupe across specialists. Score confidence 1 to 10. Apply the evidence rule: a safety claim cites the line, a "handled elsewhere" claim cites the handler, a "tests cover this" claim names the test.
6. Fix-first. AUTO-FIX for mechanical items with one right answer, ASK for judgment calls, in one batch with a recommendation. Apply approved fixes. Never commit.
7. Doc staleness check, then append one line per lasting lesson to the repo's learnings file.
8. Status: DONE, DONE_WITH_CONCERNS, BLOCKED or NEEDS_CONTEXT, with the escalation format.

Budgets: `SKILL.md` 150 lines, `checklist.md` 120, each specialist 60, each stack pack 60.

### plan-review

One skill replacing two. Modes: hold (default), expand, selective, reduce. Mode is chosen once and never drifts. Step 0 has three parts: premise challenge, existing-code leverage, and at least two implementation alternatives. Of the CEO cognitive-patterns list, only the six that map to a step survive, each as one checkable action inside its step: inversion in the premise challenge, focus-as-subtraction and speed calibration in mode selection, proxy skepticism in the premise challenge, hierarchy-as-service and edge-case paranoia in the UI section. The other eleven are dropped. Review sections load from sibling files only when relevant: architecture, errors (every error named with its trigger, catcher, user-visible result and test), security, data flow with the three shadow paths (nil, empty, upstream error), tests (every behaviour tested, no test without a regression it would catch), performance, observability, rollout and rollback. Required outputs: NOT in scope, what already exists, failure-mode registry, diagrams for every new flow, unresolved decisions. Target: 150 lines main file, 60 per section, down from the 43 KB and 14 KB files it replaces.

### pr

Keep from hushmono: merged-PR preflight (never reuse a squash-merged branch), conventional title, split suggestion above 400 lines, the gates record, the compliance note when the diff touches PII, transactions, audit logs or access control. Add from mattpocock: a summary as the smallest visual that makes the change clear, before and after evidence, and a merge danger call (one-way or two-way door, blast radius). The co-author line comes from the harness, not the template.

### test

Reads commands from the repo config. Picks what to run from changed files. Flags changed code with no test as a gap and offers to write one with `tdd`. Contains no commands of its own.

### tdd

Seams agreed with the user before any test is written. One test, one implementation, repeat. Good-test and mocking rules in sibling files. Expected values come from an independent source, never recomputed the way the code computes them.

### implement

Fetch the ticket and state its title. Call `tdd` at the agreed seams. Typecheck often, single test files often, the full suite once at the end. Call `review` when done. Stop there. The user commits after verifying on device.

### diagnose

Phase 1 is the skill: build a fast, deterministic, red-capable command before any hypothesis. Then minimise, rank three to five falsifiable hypotheses, instrument one variable at a time with tagged logs, write the regression test before the fix, clean up by grepping the tag. Flake recipe from gstack: reproduce on main in a worktree, report failed-of-N, never loosen the assertion.

### grill, spec

`grill` runs the numbered-question rounds with a recommended answer per question, and looks up facts itself instead of asking. With the glossary option on, it updates `GLOSSARY.md` and writes ADRs inline. `spec` synthesises the conversation into the repo's requirements and design templates and files it on the configured tracker.

### retro, handoff, guard, commit, setup, writing-for-agents

Ported with light edits. `retro` classifies each mistake first: mechanical ones become a lint rule, hook or CI job; judgment calls become a review rule. `setup` explores the repo, proposes the config, and writes it after confirmation.

## Repo config

`/setup` writes one file into the consuming repo, `docs/agents/skillset.md`, and adds a three-line pointer to its `CLAUDE.md`. Sections:

- tracker: GitHub issues via `gh` (repo slug), or local markdown. No Jira for now; a Jira option can be added later without changing the skills, since they only read this section.
- commands: test, lint, typecheck per area of the repo
- thresholds: coverage, function size, nesting, PR size
- docs: paths and templates for requirements, design docs, plans, ADRs, glossary, learnings
- stacks: which packs under `stacks/` are enabled
- models: subagent routing (default Haiku for reads, Sonnet for everything else)
- compliance: optional triggers that add a note to PRs

Skills read this file. They never carry a copy of its values.

## Phases

### Phase 0: scaffold (this commit)

README, PLAN, PROMPT, NOTICE, LICENSE, `.gitignore`, `docs/sources.md`. Exit: the repo exists locally and the plan is agreed.

### Phase 1: conventions, manifest, setup

Author `writing-for-agents` first and apply it to everything after. Add `.claude-plugin/plugin.json` and `marketplace.json`. Write `templates/skillset.md` and the `setup` skill. Exit: `claude plugin validate . --strict` passes, and `/setup` runs cleanly in a throwaway repo.

### Phase 2: gate side

`review`, `test`, `pr`, `commit`, plus `stacks/gcp-python`, `stacks/nextjs-bun` and `stacks/expo` review checks. Exit: `review` run against three already-merged hushmono PRs with known defects finds those defects, and the findings are compared with what the old gates reported. Candidates: the PRs behind the #3410 and #3379 lessons.

### Phase 3: build side

`grill`, `spec`, `tdd`, `implement`, `diagnose`. Exit: one real ticket taken from grill to review using only these skills.

### Phase 4: plan side and hygiene

`plan-review`, `retro`, `handoff`, `guard`. Exit: `plan-review` run on one existing hushmono design doc produces the required outputs in under 150 lines of skill text.

### Phase 5: trial and cutover

Install as a plugin in a hushmono worktree. Use it for two weeks alongside the old gates. Then, as a separate hushmono PR on Ivan's call, point CLAUDE.md step 5 at the new set and delete the old `.claude/skills` and agents.

## Evals

Each skill ships a docs page with an "It's working if" section and an `evals/<skill>/` folder: a fixture diff and the findings it must produce for `review`, a transcript of expected rounds for `grill`, a broken fixture with a known cause for `diagnose`. Run results are recorded in `docs/evals.md` with the date and model.

## Open decisions

1. Repo name and location. Decided 2026-10-12: `e-skills`, at `~/Development/e-skills`, remote `https://github.com/crystaldonut/e-skills.git` (crystaldonut account, not ivanatnine30).
2. Plugin name. Decided 2026-10-12: `e-skills`. It prefixes every skill, so `/e-skills:review` always works even when a harness ships its own `/review`.
3. Tracker. Decided 2026-10-12: GitHub via `gh` only. No Atlassian MCP, `acli` or Jira prose for now.
4. `troubleshoot`. Decided 2026-10-12: stays in hushmono as is. e-skills ships `diagnose` only.
5. CEO cognitive patterns. Decided 2026-10-12: keep only the six that map to a review step, written as actions inside those steps (see the plan-review design note). The list itself is dropped.

All five decided. Phase 1 can start.
