# Omabook workspace

The planning workspace for [Omabook](https://github.com/jellespijker/omabook),
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

## Building

On a machine with little memory, build with `bin/build` in `omabook/` (it
limits the parallel jobs) and run one build at a time.
