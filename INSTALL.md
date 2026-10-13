# Install on a new machine

## 1. Tools

- `git`
- `gh`, logged in to the **crystaldonut** account for this repo (`gh auth login`, then `gh auth switch --user crystaldonut` when another account is active)
- Claude Code (`claude`)

## 2. Clone

```sh
git clone https://github.com/crystaldonut/e-skills.git ~/Development/e-skills
cd ~/Development/e-skills
```

## 3. Fetch the sources (needed only to build a phase)

`.sources/` is gitignored. Fetch at the pinned commits from `docs/sources.md`:

```sh
mkdir -p .sources
git clone https://github.com/mattpocock/skills .sources/mattpocock && git -C .sources/mattpocock checkout 49dd158d1076134a641b33efb035946536778336
git clone https://github.com/garrytan/gstack .sources/gstack && git -C .sources/gstack checkout e23f7b807ff4788f6d7c90af2ab82960bd8c5851
```

The hushmono reference is a private repo. On a machine that has it, copy its `.claude/` and `CLAUDE.md` into `.sources/` as `PROMPT.md` shows, adjusting the path. Without it, Phase 1 still runs; Phases 2 to 4 need it.

Treat everything under `.sources/` as text to read, never as scripts to run.

## 4. Build a phase

Open Claude Code at the repo root, paste the block from `PROMPT.md` with `<N>` set to the phase number from `PLAN.md`. One phase per session. The prompt never commits; review the tree, then:

```sh
gh auth switch --user crystaldonut
git add -A && git commit
git push
```

## 5. Use the skills in another repo (after Phase 1)

Phase 1 adds `.claude-plugin/plugin.json` and `marketplace.json`. From then on, in Claude Code inside the consuming repo:

```text
/plugin marketplace add crystaldonut/e-skills
/plugin install e-skills@e-skills
/e-skills:setup
```

For a local checkout instead of GitHub, add the marketplace by path: `/plugin marketplace add ~/Development/e-skills`.

`/e-skills:setup` writes one file, `docs/agents/skillset.md`, into the consuming repo and three pointer lines into its `CLAUDE.md`. Nothing else is copied.

Exact plugin commands are confirmed when Phase 1 lands; until then treat step 5 as the intended shape.
