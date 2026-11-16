# Omabook workspace

The main workspace for developing Omabook and its plugins, and the planning workspace for [Omabook](https://github.com/jellespijker/omabook),
the ebook library and reader for Omarchy, and its
[Storyteller plugin](https://github.com/jellespijker/omabook-storyteller).
It holds the shared Kanban board configuration (`.herdr-kanban.toml`) for both
repositories; the code lives in each repository.

## Set up

```bash
gh repo clone jellespijker/omabook-workspace && cd omabook-workspace
herdr-kanban sync-repos     # clones omabook and omabook-storyteller here
herdr-kanban board          # the board: Triage, Ready, In Progress, Review, Done
```

Tickets are named by repository: `omabook#12`, `storyteller#3`. A ticket is
worked on in its own worktree, which can read the other repository under
`.siblings/`. A ticket lands on `main` only after that repository's tests pass.

## Labels and milestones

Every ticket carries one `type:*` and at least one `domain:*` label and a project `Priority`
(`P0`–`P3`); the facets live in `.herdr-kanban.toml` and `herdr-kanban sync-labels --cwd <repo>`
provisions them. Milestones are release versions: Omabook `0.1.6`, `0.1.7`; Storyteller
`1.3`, `1.4`. Agents: see [AGENTS.md](AGENTS.md).

## Packaging

`omabook-packaging/` is a symlink to `../omabook-packaging`, the PKGBUILD recipes for
Omarchy and the AUR, in a Git repository of its own (local, not on GitHub) and not on the board.
Its README lists what to update on each Omabook release.

## Building

On a machine with little memory, build with `bin/build` in `omabook/` (it
limits the parallel jobs) and run one build at a time.
