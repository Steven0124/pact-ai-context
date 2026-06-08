# AI Context — Entry Point

This file is the entry point for any AI assistant (Claude, Gemini, Codex, Cursor, …) working in this repo. It is intentionally short — it points to where the real content lives. Read the files that match the task at hand; don't load everything at once.

This repo is a **PACT** context system: four modules that give you persistent working memory across sessions.

```
projects/   → P — active initiatives, current state, next steps   (volatile)
agenda/     → A — rolling daily execution board                    (volatile)
domains/    → C — Context: long-term system & domain knowledge     (stable)
worklog/    → T — Timeline: dated audit trail of what shipped       (frozen)
```

## Behavioural cues

### Session start: orient

Read these first, and only these:
1. [`PROFILE.md`](PROFILE.md) — who you're working with: role, stack, working style, and any guardrails that need human sign-off. Read this once so you don't have to ask.
2. [`projects/STATUS.md`](projects/STATUS.md) — a single-file digest of every active / blocked / review project. Tells you what's in flight, where it's stuck, what's next.
3. [`agenda/AGENDA.md`](agenda/AGENDA.md) — the day-to-day tactical task list.

**Don't open individual project, domain, or worklog files unless a deeper question demands it.** PROFILE.md, STATUS.md, and AGENDA.md are the orientation surface.

### During session: keep projects current

When work happens that changes the state of a known project (a PR ships, a blocker resolves, a decision is made, a sub-task starts/finishes), **suggest an update** — append to the project's Timeline section, bump `Last updated`, adjust Status if needed. **If the change affects the project's headline** (Status / Target / current-state one-liner / next milestone), **also update `projects/STATUS.md`**. Don't auto-edit without confirming. If `Last updated` on an active project is more than 30 days old, flag it.

### During session: capture work worth remembering

**Notice when work worth recording is happening** — a PR opened/merged, a bug root-caused, an incident handled, a design decision made. **Before the session winds down, ask once:** "Worth adding a worklog entry for this?" If yes:

1. Create a new entry under `worklog/entries/` named `YYYY-MM-DD-<short-slug>.md`, using the schema in [`worklog/README.md`](worklog/README.md).
2. Append a one-line bullet to the current month's index file (e.g. `worklog/2026-06.md`).

Don't pester for routine work. One discrete thing → one entry; a session can produce zero, one, or several.

### Project lifecycle

When a project hits `shipped` or `dropped`, **don't auto-archive** — walk the user through the decision: archive the file (substantial initiative worth a history), fold it into `domains/` (it ended as stable system behaviour), or delete it (a worklog entry already covers it). See [`projects/README.md`](projects/README.md).

### Agenda lifecycle

[`agenda/AGENDA.md`](agenda/AGENDA.md) is a rolling board. If it contains days older than ~7 days, move them to `agenda/archive/YYYY-MM.md`. Roll any uncompleted `[ ]` tasks from those old days forward to today before archiving.

## Trigger phrases (user → AI)

- "What should we focus on today?" / "What am I working on?" → read STATUS.md + AGENDA.md, summarise.
- "Where am I on `<project>`?" → open that project file, summarise current state + next steps + blockers.
- "Update `<project>`" → propose timeline + status changes from recent context.
- "`<project>` is done" / "Archive `<project>`" → walk the lifecycle decision.

## How to maintain this repo

- Keep notes focused and small. Many short files beat one giant file.
- Use plain markdown links so any AI tool can follow them.
- Keep this entry file short — it's an index, not a manual. The detail lives in each module's `README.md`.
