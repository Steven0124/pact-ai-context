# A — Agenda

The rolling daily execution board. **Volatile** — rewritten as days pass. Where `STATUS.md` holds high-level project milestones, the Agenda holds the concrete *"what needs doing today and tomorrow"* — across all projects, plus ad-hoc tasks that don't belong to any project.

## Layout

```
agenda/
├── README.md           # this file
├── AGENDA.md           # the live board — current + recent days
└── archive/
    └── YYYY-MM.md       # past days, rolled off after ~7 days
```

## How it works

- [`AGENDA.md`](AGENDA.md) is organised newest-day-first, one `##` heading per day.
- Under each day, group tasks by project or theme, as `[ ]` / `[x]` checkboxes.
- Keep it short — it's a working board, not a historian. Anything worth remembering long-term becomes a [`worklog/`](../worklog/) entry; anything that's a system fact becomes a [`domains/`](../domains/) note.

## Lifecycle

When `AGENDA.md` accumulates days older than ~7 days:
1. **Roll forward** any uncompleted `[ ]` tasks from those old days into today.
2. **Move** the old day blocks into `archive/YYYY-MM.md`.

The AI should do this automatically when it notices stale days at session start.
