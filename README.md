# P.A.R.K.I.T — Project Management

This repository contains project-management documentation and working materials for **P.A.R.K.I.T** , an application for reserving parking spaces in the office parking area.

It is used to track the project context, current work, research, open questions, risks, and decisions while the project is being developed.

---

## Current Focus

1. **LED Matrix Integration** — research and evaluation
2. **Administration Approval** — in progress
3. **Expiring Reservation Reminder** — planned

See:
- [`PROJECT_ROADMAP.md`](PROJECT_ROADMAP.md) — project direction and phases
- [`CURRENT_TASKS.md`](CURRENT_TASKS.md) — current high-level work
- `Project board` — tasks, owners, and progress

---

## Repository Structure

```text
management/
├── README.md
├── PROJECT_ROADMAP.md
├── CURRENT_TASKS.md
│
├── project-context/
│   ├── mind-map/
│   └── glossary/
│
├── project-notes/
│   ├── meeting-notes.md
│   ├── problems.md
│   ├── risks.md
│   ├── open-questions.md
│   └── decisions.md
│
└── workstream/
    ├── led-integration/
    ├── project-presentation/
    └── reservation-reminder/
```

---

## Where Information Belongs

| Information | Location |
|---|---|
| Project direction and phases | [`PROJECT_ROADMAP.md`](PROJECT_ROADMAP.md) |
| Current high-level work | [`CURRENT_TASKS.md`](CURRENT_TASKS.md) |
| Tasks, owners, and progress | `Project Board` |
| Problems | [`project-notes/problems.md`](project-notes/problems.md) |
| Open questions | [`project-notes/open-questions.md`](project-notes/open-questions.md) |
| Risks | [`project-notes/risks.md`](project-notes/risks.md) |
| Decisions | [`project-notes/decisions.md`](project-notes/decisions.md) |
| Meeting outcomes | [`project-notes/meeting-notes.md`](project-notes/meeting-notes.md) |
| Project context and terminology | [`project-context/`](project-context/) |
| Research and working materials | [`workstream/`](workstream/) |
| Final technical documentation | [`parkit-service` repository](https://github.com/berufsbildung-basel/parkit-service) |

---

## Documentation Rules

- Avoid duplicating information between files.
- Keep meeting notes short; actions belong in the `project board`.
- Keep research inside the relevant [`workstream/`](workstream/).
- Record confirmed decisions in [`decisions.md`](project-notes/decisions.md).
- Mark unconfirmed information as `TBD`.
- Move finalized technical documentation to the main [`parkit-service`](https://github.com/berufsbildung-basel/parkit-service) repository.