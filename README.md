# pact-ai-context

A minimal, file-based context system that gives an AI coding assistant (Claude, Gemini, Codex, Cursor, …) persistent working memory across sessions. (Read the background and design philosophy in the [LinkedIn post](https://www.linkedin.com/posts/steven-nam-onn-fatt_para-ai-aicontext-share-7469795051867414528-IBl3/?utm_source=share&utm_medium=member_ios&rcm=ACoAADTkyisB1Np8RMp1s-xc886f8QdRsbZFM6g)).

Point your AI tool at this folder and it can answer five questions before you type anything: who am I, what am I working on, what matters today, how does the system work, and what already happened. A top-level [`PROFILE.md`](PROFILE.md) answers the first ("who"); the four PACT modules below answer the rest. This repository is a barebones template — fork it, delete the example content, and fill it with your own work.

## The PACT structure

Four top-level modules, one per question:

| Module | Folder | Holds | Changes |
|---|---|---|---|
| **P — Projects** | [`projects/`](projects/) | Active initiatives: current state, next steps, blockers. Includes a single-file [`STATUS.md`](projects/STATUS.md) digest the AI reads first. | Often |
| **A — Agenda** | [`agenda/`](agenda/) | A rolling daily execution board: today/tomorrow's tasks across all projects, plus ad-hoc work. | Daily |
| **C — Context** | [`domains/`](domains/) | Long-term system knowledge: architecture, domain logic, conventions, decisions. | Rarely |
| **T — Timeline** | [`worklog/`](worklog/) | A dated, append-only audit trail of what shipped, what broke, and what was decided. | Append-only |

Each module has a `README.md` describing its schema and lifecycle, plus an `example-*` file showing the shape. The design separates current state (Projects) from history (Timeline), and long-term knowledge (Context) from day-to-day execution (Agenda).

> The Context and Timeline modules live in folders named `domains/` and `worklog/` — the names most engineers already reach for. The PACT letters are the concept; the folder names are what you'll type.

## Repository layout

```
pact-ai-context/
├── CLAUDE.md             # AI entry point — what to read at session start, how to keep files current
├── README.md
├── PROFILE.md            # who the AI is working with — role, stack, working style, guardrails
├── projects/             # P — active initiatives
│   ├── README.md
│   ├── STATUS.md         #     single-file digest, read first
│   ├── example-project.md
│   └── archive/          #     frozen shipped/dropped projects
├── agenda/               # A — rolling daily execution board
│   ├── README.md
│   ├── AGENDA.md
│   └── archive/          #     past days, rolled off after ~7 days
├── domains/              # C — long-term system knowledge (Context)
│   ├── README.md
│   └── example-domain.md
└── worklog/              # T — dated audit trail (Timeline)
    ├── README.md
    ├── 2026-06.md        #     monthly index, one line per entry
    └── entries/
        └── 2026-06-09-example-entry.md
```

## Getting started

1. **Fork or clone** this repository.
2. **Fill in `PROFILE.md`** with who you are, and **delete the example files** (`example-project.md`, `example-domain.md`, the example worklog entry, and the sample day in `AGENDA.md`). Keep each module's `README.md` and `projects/STATUS.md` — those define the schema and the orientation surface.
3. **Wire it to your AI tool.** [`CLAUDE.md`](CLAUDE.md) is the entry point that tells the assistant what to read at session start. Most tools auto-load a file like this; rename or symlink it to whatever yours expects (`GEMINI.md`, `.cursorrules`, `AGENTS.md`, …).
4. **Start using it.** Open a session with "what should we focus on today?" and let the assistant read `projects/STATUS.md` and `agenda/AGENDA.md`. As work progresses, it keeps the project files, agenda, and worklog current.

## Conventions

- **Markdown only.** Plain `.md` files and plain markdown links, so any tool can read and follow them.
- **Many small files** beat one large file.
- **`STATUS.md` and `AGENDA.md` are the orientation surface** — the assistant reads those at session start and only opens individual files when a deeper question demands it.
- **Lifecycle is handled per module** — see each module's `README.md`. In short: stale agenda days roll into `agenda/archive/`; finished projects are archived, folded into `domains/`, or deleted; worklog entries are never edited once written.
