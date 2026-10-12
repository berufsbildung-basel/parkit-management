# P.A.R.K.I.T — Project Management

This repository contains project-management documentation and working materials for **P.A.R.K.I.T**, an application for reserving parking spaces in the office parking area.

It is used to track the project context, current work, research, open questions, risks, and decisions while the project is being developed.

Finalized technical documentation and implementation belong in the main `parkit-service` repository.

---

## Current Focus

The project is currently focused on:

1. **LED Matrix Integration** — research and evaluation in progress.
2. **Administration Approval** — preparation for Facility Management approval.
3. **Expiring Reservation Reminder** — planned.

See [`CURRENT_TASKS.md`](CURRENT_TASKS.md) for the current high-level status.

See [`PROJECT_ROADMAP.md`](PROJECT_ROADMAP.md) for the overall project direction and major phases.

Detailed tasks, subtasks, owners, and progress are managed in the project task tracker.

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
└── workstreams/
    ├── led-integration/
    ├── administration-approval/
    └── reservation-reminder/
```

---

## Where Information Belongs

| Information | Location |
|---|---|
| Overall project direction and phases | `PROJECT_ROADMAP.md` |
| Current high-level work | `CURRENT_TASKS.md` |
| Detailed tasks, subtasks, owners and progress | Project task tracker |
| Project problems | `project-notes/problems.md` |
| Open questions | `project-notes/open-questions.md` |
| Project risks | `project-notes/risks.md` |
| Decisions and their rationale | `project-notes/decisions.md` |
| Short meeting outcomes | `project-notes/meeting-notes.md` |
| Project terminology | `project-context/glossary/` |
| Project overview and relationships | `project-context/mind-map/` |
| Research and intermediate work | Relevant `workstreams/` directory |
| Final technical documentation | Main `parkit-service` repository |

---

## Workstreams

Each major area of work has its own directory under `workstreams/`.

A workstream should contain:

- its goal and problem;
- scope;
- requirements where relevant;
- expected outcome;
- research and working materials;
- links to related tasks and decisions.

Research and intermediate materials may change while the work is in progress.

Once a technical solution is validated and finalized, the relevant documentation should be transferred to the main `parkit-service` repository.

---

## Working Principles

- Do not duplicate detailed task tracking in this repository.
- Record unresolved questions as open questions, not decisions.
- Record potential future problems as risks.
- Record confirmed decisions separately from research and assumptions.
- Keep meeting notes short and move resulting actions to the task tracker.
- Keep research inside the relevant workstream.
- Mark unknown or unconfirmed information as `TBD`.