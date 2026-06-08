# P — Projects

Active state for ongoing initiatives. **Volatile** — these files change as work progresses. The point: any AI assistant opening a fresh session should know *"what am I working on right now, where is it stuck, what's next"* without being told from scratch.

## Layout

```
projects/
├── README.md           # this file
├── STATUS.md           # single-file digest — the AI reads this at session start
├── <slug>.md           # one file per active initiative (source of truth)
└── archive/
    ├── README.md       # index of completed / dropped projects (newest first)
    └── <slug>.md       # frozen shipped / dropped project files
```

## STATUS.md — the orientation file

[`STATUS.md`](STATUS.md) is a single-file digest of every project with status `active` / `blocked` / `review`. **This is what the AI reads at session start** so it doesn't have to open every project file. Per project:

- Linked title
- `**Updated:**` date · `**Target:**` (if set)
- One-line current state ("Now:")
- One-line next milestone ("Next:")

**Update STATUS.md whenever a project's headline changes** — Status, Target, current-state summary, or the immediate next milestone. Don't keep full timelines / blockers / detailed next-steps in sync there — those live in the individual project files.

## How `projects/` differs from `domains/` and `worklog/`

| Module | Captures | Time-feel | Update cadence |
|---|---|---|---|
| `domains/<topic>.md` | How the system works (stable knowledge) | Stable | Rare — only when the system changes |
| **`projects/<slug>.md`** | **Where I am, what's next, what's blocked** | **Volatile** | **Often — every meaningful state change** |
| `worklog/entries/<date>-<slug>.md` | What I did on date X | Frozen once written | One-shot per event |

## Schema for an active project file

```markdown
# <Project name>

- **Status:** active | blocked | review | shipped | dropped
- **Domain:** [<related-domain-file>](../domains/<file>.md)
- **Last updated:** YYYY-MM-DD
- **Target:** YYYY-MM-DD (optional — set once a date is committed)

## Current state
One paragraph. Where are we *right now*. First sentence should answer "is this moving, stuck, or done?"

## Next steps
- [ ] Action item (owner if not me)
- [ ] Action item

## Open blockers / decisions
- **Blocker name** — who's needed, since when (YYYY-MM-DD), what unblocks it
- **Decision pending** — options on the table, who decides

## Timeline
- **YYYY-MM-DD** — event (PR shipped, decision made, blocker raised/resolved)
- **YYYY-MM-DD** — event

## Related
- Domain: <domain-note-slug>
- Worklog entries: YYYY-MM-DD-slug, YYYY-MM-DD-slug
```

## Lifecycle: what happens when a project ends

When a project hits `shipped` or `dropped`, decide where the value lives:

| Project type | What to do | Why |
|---|---|---|
| **Substantial initiative** (multi-week, several sub-tasks, real decisions) | **Move file to `archive/<slug>.md`**, freeze the timeline, set status | The decision history is worth keeping |
| **Small project** (1–2 PRs, no complex state) | **Delete the project file** | Timeline entries already capture it |
| **Ends as stable system behaviour** | **Fold into `domains/<topic>.md`** | Stable knowledge belongs in Context, not the archive |

Heuristic: *"Three years from now, if I ask 'how did I drive this?', do I want one file that answers it?"* → archive. *"Do I just want to know how the system looks today?"* → domain note. *"Was it just a PR?"* → worklog entry.

## AI behaviour expectations

1. **Session start.** Read [STATUS.md](STATUS.md) only. Open an individual project file only when a deeper question demands it.
2. **During session.** On a state change (PR ships, blocker resolves, decision made, sub-task starts), **suggest an update** — append to Timeline, bump `Last updated`, adjust Status. If the headline changes, **also update STATUS.md**.
3. **End of session.** If state changed and the file wasn't touched, prompt once: "Update `<project>.md` before we wrap?"
4. **When a project finishes.** Walk the user through the lifecycle table. Don't auto-archive.
5. **Don't let files go stale silently.** Flag any `active` project whose `Last updated` is more than 30 days old.
