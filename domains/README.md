# C — Context (`domains/`)

Long-term system memory — the **Context** module of PACT, kept in a folder named `domains/`. **Stable** — these notes change rarely, only when the underlying system does. This is where the AI learns *how things actually work*: architecture, domain logic, conventions, integration quirks, and the reasoning behind past structural decisions.

Think of it as the documentation you wish existed when you joined — written for an assistant that needs to reason over it, not just read it.

## Layout

```
domains/
├── README.md           # this file (also the index of notes)
└── <topic>.md          # one note per topic / domain / system
```

List each note below as you add it, so the index stays useful.

## Notes

- [example-domain](example-domain.md) — placeholder showing the shape of a domain note (delete once you add real ones)

## What belongs here (vs. Projects / Worklog)

| Belongs in Context | Belongs elsewhere |
|---|---|
| How a subsystem works, and why it's built that way | Where a piece of work currently stands → `projects/` |
| Conventions, patterns, gotchas that outlive any one task | What you did on a given day → `worklog/` |
| Architecture decisions that are now just "how it is" | Today's to-do list → `agenda/` |

When a project ends as *stable system behaviour* (not just a shipped task), fold its lasting knowledge into a domain note rather than archiving the project file.

## Schema (loose — these are prose notes)

```markdown
# <Topic>

Short statement of what this covers and why it matters.

## How it works
The mechanics. Diagrams-in-words, data flow, key components.

## Conventions / gotchas
Things that bite you if you don't know them.

## Decisions & rationale
Why it's built this way; alternatives that were ruled out.

## Related
- Projects: <slug>
- Other domains: <slug>
```
