# AGENTS.md — Omabook workspace

This workspace is the main place to develop Omabook and its plugins. Work here, not in
a separate clone of `omabook` or `omabook-storyteller`.

| Path | Repository | Board alias |
|---|---|---|
| `omabook/` | [jellespijker/omabook](https://github.com/jellespijker/omabook), the app | `omabook` |
| `omabook-storyteller/` | [jellespijker/omabook-storyteller](https://github.com/jellespijker/omabook-storyteller), the Storyteller plugin | `storyteller` |
| `omabook-packaging/` | symlink to `../omabook-packaging`: PKGBUILD drafts; not a git repo, not on the board | — |

Each repository keeps its own history, issues and milestones. This repository holds only the
shared board configuration (`.herdr-kanban.toml`) and these notes. `herdr-kanban sync-repos`
clones the two repositories here.

## Start of a session

```bash
herdr-kanban board          # Triage, Ready, In Progress, Blocked, Review, Done
herdr-kanban inbox --ack
```

Board: <https://github.com/users/jellespijker/projects/8>. Tickets are named by alias:
`omabook#12`, `storyteller#3`. Claim a ticket (`herdr-kanban claim omabook#12`) before a
non-trivial change; it gets its own worktree, which can read the other repository under
`.siblings/`. Deposit bugs and follow-ups you find with `herdr-kanban deposit` instead of
fixing them off the ticket. A ticket lands on `main` only after its repository's
`check_command` (see `.herdr-kanban.toml`) passes.

## Labels, priority, milestones

- Every ticket needs one `type:*` (`feature`, `bug`, `doc`, `chore`, `spike`) and at least one
  `domain:*` (`library`, `reader`, `metadata`, `sync-share`, `ai-mcp`, `plugins`,
  `packaging-release`, `telemetry`, `accessibility`, `dx`), plus a `Priority` (`P0`–`P3`) on the
  project, before it is Ready.
- The facets are defined in `.herdr-kanban.toml`; `herdr-kanban sync-labels --cwd <repo>`
  provisions them in a repository. Do not invent labels.
- Milestones are release versions: Omabook `0.1.6`, `0.1.7`, …; Storyteller `1.3 (with Omabook
  0.1.5)`, `1.4 (with Omabook 0.1.6)`, … Put a ticket in the release it should ship in.

## Commits

Every commit message contains the number of the GitHub issue it belongs to, in the subject or the
body: `Turn whole pages, or scroll on through the chapters (#26)`. Write `#12` in the repository
that owns the issue, so GitHub links it, and `jellespijker/omabook#12` from any other repository.
If there is no issue for the work, deposit one (`herdr-kanban deposit`) before you commit.

## Rules that span both repositories

- Storyteller needs the Omabook version named in its milestone; when a Storyteller change needs
  a new Omabook feature, open the Omabook ticket first and link them.
- Build Omabook with `omabook/bin/build`, one build at a time (see `omabook/AGENTS.md`).
- Each repository has a harness (`.agents/`, rules in `.agents/rules/`) that checks every edit and
  commit; run `uvx pre-commit install` once in each clone, and `bin/check` before handing work in.
- Each repository's `AGENTS.md` and README apply inside it; this file applies to the whole workspace.
