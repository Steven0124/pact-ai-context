# T — Timeline (`worklog/`)

The dated audit trail — the **Timeline** module of PACT, kept in a folder named `worklog/`. **Frozen** — entries are written once and not edited. A rolling record of work worth remembering: shipped PRs, root-caused bugs, incidents handled, decisions made. Great for standups, retros, self-reviews, or just reconstructing *"what did I actually do this quarter?"*

## Layout

```
worklog/
├── README.md                          # this file
├── YYYY-MM.md                          # monthly index — one bullet per entry
└── entries/
    └── YYYY-MM-DD-<short-slug>.md       # one file per discrete thing
```

- **One file per entry** in `entries/`, named `YYYY-MM-DD-<short-slug>.md`.
- **One monthly index file** at the root, one bullet per entry with a one-line hook. Indexes are what you scan; entries hold the detail.

## Filename convention

`YYYY-MM-DD-<kebab-slug>.md` — date the work happened/shipped; slug is 2–5 lowercase hyphenated words. Use the feature/topic name, not PR numbers.

- Good: `2026-06-09-checkout-cache.md`
- Bad: `2026-06-09-pr-1234.md`, `2026-06-09-stuff.md`

## Schema for an entry

```markdown
# YYYY-MM-DD — <short title>

- **Type:** feature | bugfix | incident | design | review | ops
- **Tickets/PRs:** TICKET-123, repo#456
- **Project:** <project-slug> (if applicable)

## What
1–2 short paragraphs on the substance. Enough that future-you can reconstruct the work without re-reading the PR.

## Artifacts
- PR(s) with URL
- Doc / ADR / dashboard link if applicable

## Related
- YYYY-MM-DD-other-entry
```

## Monthly index format

`YYYY-MM.md` is a thin index — one bullet per entry: `[date — title](path)` — `type · scope · one-line hook`.

```markdown
# Worklog — June 2026

- [2026-06-09 — Cached the pricing lookup](entries/2026-06-09-example-entry.md) — feature · checkout · cut p95 by moving pricing behind a 30s cache
```

## What's worth recording

**Yes:** a non-trivial PR merged; a bug with real impact fixed; an incident handled; a design/architecture decision; a review that shifted direction; a hard problem debugged; cross-team unblocking.

**No:** routine reads, casual questions, trivial typo/dependency bumps, conversations about maintaining this repo itself.

## AI behaviour expectations

1. **Notice** during a session when record-worthy work happens (PR merged, bug root-caused, incident engaged, decision made).
2. **Before the session winds down, ask once:** "Worth adding a worklog entry for this?"
3. If yes: **create the entry** under `entries/` and **append a bullet** to the month's index.
4. **Don't pester** for routine work. **One entry per discrete thing**, not one per session.
