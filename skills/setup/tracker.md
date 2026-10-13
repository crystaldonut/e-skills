<!-- source: mattpocock/skills@49dd158 skills/engineering/setup-matt-pocock-skills/issue-tracker-github.md, issue-tracker-local.md -->

# Tracker blocks

One of these becomes the `## Tracker` section of `docs/agents/skillset.md`. Copy the block under the chosen heading and fill the angle brackets.

## GitHub

```markdown
GitHub issues on `<owner>/<repo>`, through the `gh` CLI.

- **Fetch the ticket**: `gh issue view <number> --json number,title,body,labels,comments`.
- **Publish to the tracker**: `gh issue create --title "..." --body "..."`, with a heredoc for a multi-line body.
- **Comment**: `gh issue comment <number> --body "..."`.
- **Close**: `gh issue close <number> --comment "..."`.
- Issues and pull requests share one number space. Resolve a bare `#42` with `gh pr view 42`, then `gh issue view 42`.
```

## Local markdown

```markdown
Markdown files under `.scratch/`, one directory per feature.

- The spec is `.scratch/<feature-slug>/spec.md`.
- Each ticket is its own file, `.scratch/<feature-slug>/issues/<NN>-<slug>.md`, numbered from `01`.
- A `Status:` line near the top of a ticket holds its state: `open`, `claimed` or `resolved`.
- **Fetch the ticket**: read the file at the path or number the user gives.
- **Publish to the tracker**: create the file, and its directory when missing.
- **Comment**: append under a `## Comments` heading at the bottom of the file.
- **Close**: set `Status: resolved`.
```
