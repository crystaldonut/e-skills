# Expected outcome

Prepare: copy `fixture/` to a scratch directory outside this repo, then `git init`, `git remote add origin https://github.com/example/setup-fixture.git`, `git add -A`, `git commit -m fixture`.

Run `/e-skills:setup` there and accept every recommended answer.

After the run:

1. `git status --short` lists exactly ` M CLAUDE.md` and `?? docs/` (holding `docs/agents/skillset.md` only).
2. The config's tracker section is the GitHub block with the slug `example/setup-fixture`.
3. The commands table has one row: test `npm test` or `npm run test`, lint `npm run lint`, typecheck `npm run typecheck`. An equivalent runner invocation of the same three scripts passes.
4. Coverage, function length and nesting are `unset`. PR size is 400.
5. Every docs row is `unset`. Stacks is `none`. Models are haiku and sonnet.
6. `CLAUDE.md` keeps its `## Conventions` section unchanged and gains one `## Agent skills` block naming `docs/agents/skillset.md`.
7. The proposal shown before writing named `package.json` as the source of the commands.

Second run, same directory: the config and the block are updated in place, with one `## Agent skills` heading in `CLAUDE.md`.
