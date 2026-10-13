# e-skills

One set of Claude Code skills, owned here, built from three sources and tied to none of them:

| Source | What it contributes | Pinned at |
|---|---|---|
| hushmono `.claude/` (NINE30-Inc/hushmono) | The gate chain in use today: `/test`, `/paranoid-review`, `/pr`, `/commit`, senior-qa and fullstack reviewer agents, `/ceo-review`, `/eng-review`, `/investigate`, `/dispatch` | `d207f16ce` |
| garrytan/gstack (MIT) | The review pipeline as it stands today: gate integrity, sideways sibling checks, forced-critical rules, specialist subagents, fix-first flow, confidence and evidence rules | `e23f7b8` (2026-10-11) |
| mattpocock/skills (MIT) | Build-side discipline: grilling, TDD at agreed seams, diagnose-by-feedback-loop, retro, PR evidence, and the writing-for-agents rules that keep every file here short | `49dd158` (2026-10-09) |

The hushmono gates are themselves a March 2026 snapshot of gstack, so this repo is partly a refresh of that lineage and partly a merge with a different philosophy.

## Principles

1. **Text only.** A skill is a `SKILL.md` plus optional reference files. No daemon, no telemetry, no update check, no generated preambles.
2. **Short files.** Each `SKILL.md` stays under 150 lines. Reference material sits behind a pointer and loads only when needed.
3. **The environment is the source of truth.** Skills never cache commands. A per-repo config file names the test, lint and typecheck commands, the tracker and the docs paths.
4. **Evidence or unverified.** A review claim cites a file and line. "Probably handled" is not a finding.
5. **Skills never commit, push or open PRs on their own.** Only `/commit` and `/pr` do, and only when the user runs them.
6. **Subagents run on Sonnet or Haiku.** Opus is never a subagent model. The repo config can override this.
7. **Stack-agnostic core, stack packs for specifics.** Firestore, BigQuery, Cloud Functions, Next.js and Expo checks live under `stacks/` and are enabled per repo.
8. **Every ported file names its source** in frontmatter. `NOTICE.md` carries the MIT notices.

## Layout

```
skills/<name>/SKILL.md        one skill, with sibling reference files when needed
stacks/<stack>/               checks and commands for one technology stack
templates/                    what /setup writes into a consuming repo
docs/<skill>.md               What it does / When to reach for it / It's working if
evals/<skill>/                fixtures and expected outcomes
.claude-plugin/               plugin.json and marketplace.json
PLAN.md                       the build plan, phase by phase
PROMPT.md                     the prompt that builds a phase
NOTICE.md                     attribution
INSTALL.md                    set up a new machine, build a phase, install the plugin
```

## Status

Phase 0, scaffold only. See `PLAN.md` for the phases and `PROMPT.md` to run one.

## Installing later

See `INSTALL.md`: clone, fetch the sources, build a phase, and (after Phase 1) install as a Claude Code plugin from GitHub or a local path, then run `/e-skills:setup` once.
