# Sources

Pinned commits and what is taken from each. Fetch into `.sources/` with the commands in `PROMPT.md`.

## mattpocock/skills at 49dd158 (2026-10-09)

| File | Used by | Take | Leave |
|---|---|---|---|
| `skills/productivity/writing-for-agents/SKILL.md`, `SKILL-MECHANICS.md` | `writing-for-agents`, every other skill | all of it | nothing |
| `skills/productivity/grilling/SKILL.md` | `grill` | round format, frontier, facts are the agent's job | nothing |
| `skills/engineering/domain-modeling/*` | `grill` (option) | glossary and ADR formats | nothing |
| `skills/engineering/to-spec/SKILL.md` | `spec` | seams first, spec template | GitHub publish step, triage label |
| `skills/engineering/tdd/SKILL.md`, `tests.md`, `mocking.md` | `tdd` | all of it | nothing |
| `skills/engineering/implement/SKILL.md` | `implement` | order of operations | the commit line |
| `skills/engineering/diagnosing-bugs/SKILL.md` | `diagnose` | phases 1 to 6, redaction | the HITL script |
| `skills/engineering/code-review/SKILL.md` | `review` | the spec axis, parallel subagents, "do not rerank across axes" | the Fowler smell list (maintainability specialist covers it) |
| `skills/engineering/pr/SKILL.md` | `pr` | summary visuals, evidence tiers, merge danger | nothing |
| `skills/engineering/retro/SKILL.md` | `retro` | categories, mechanical-vs-judgment classification | nothing |
| `skills/productivity/handoff/SKILL.md` | `handoff` | all of it | nothing |
| `skills/engineering/setup-matt-pocock-skills/*` | `setup` | explore, propose, confirm, write, GitHub tracker template | GitLab tracker template, triage labels |

## garrytan/gstack at e23f7b8 (2026-10-11)

| File | Used by | Take | Leave |
|---|---|---|---|
| `review/checklist.md` | `review` | two-pass structure, gate integrity (RH tags), sideways siblings, forced CRITICAL, "do not flag" list, fix-first heuristic | citations to gstack binaries, decision-search |
| `review/specialists/*.md` | `review` specialists | each category's checks, cut to 60 lines | runtime references, telemetry |
| `review/sections/review-army.md` | `review` | dispatch shape for parallel specialists | model overlays |
| `review/SKILL.md` | `review` | confidence calibration, pre-emit verification gate, cross-review dedup, learnings capture | preamble, plan mode protocol, Greptile, Codex, artifacts sync, telemetry |
| `investigate/SKILL.md` | `diagnose` | flake recipe | hooks, edit boundary |
| `learn/SKILL.md` | `retro` | learnings file shape | runtime |
| `plan-ceo-review/SKILL.md`, `plan-eng-review/SKILL.md` | `plan-review` | only to check what changed since the hushmono copy | everything the hushmono copy already has |

## hushmono at d207f16ce

| File | Used by | Take | Leave |
|---|---|---|---|
| `.claude/skills/paranoid-review/SKILL.md` | `review` | Step 0 base branch, scope drift, two-pass categories, fix-first, verification of claims, status protocol | Rails example |
| `.claude/agents/senior-qa-engineer.md` | `review` testing specialist | tests-only constraint, failing test per bug, no `.only`/`.skip`, isolation | persona prose, Opus pin, gcloud commands, coverage numbers (move to config) |
| `.claude/agents/fullstack-code-reviewer.md` | `review` maintainability specialist | output format, "would a new team member understand this" | metrics (move to config), persona prose |
| `.claude/skills/ceo-review/SKILL.md`, `eng-review/SKILL.md` | `plan-review` | modes, prime directives, sections, required outputs | cognitive-patterns lists (decide in Phase 4), base-branch step |
| `.claude/commands/pr.md` | `pr` | preflight, gates record, compliance note, size rule | hard-coded gate names |
| `.claude/commands/commit.md` | `commit` | preflight, format, types table | the hard-coded co-author line |
| `.claude/commands/test.md` | `test` | changed-file heuristics, gap flagging | every command (move to config) |
| `.claude/commands/troubleshoot.md`, `.claude/agents/troubleshooter.md` | nothing | nothing | all of it, stays in hushmono (decision 4) |
| `.claude/skills/investigate/SKILL.md` | `diagnose` | iron law wording | phase order (diagnose builds the loop first) |
| `.claude/skills/dispatch/SKILL.md` | `implement`, config | fresh-agent-over-resume, state in git, verify every gate claim | the Opus history |
| `.claude/skills/guard/SKILL.md` | `guard` | all of it | nothing |
| `.claude/docs/commands.md`, `CLAUDE.md` | `setup` template | shape of a commands section, conventions table | values |
