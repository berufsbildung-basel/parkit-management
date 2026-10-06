## LED Matrix Integration

### Goal

Integrate LED displays with Parkit so that drivers can clearly identify the parking space assigned to their reservation.

---

### Scope

This work covers the technical preparation required for the LED integration:
- understand the basics of LED matrix systems;
- evaluate the hardware already available for the project;
- determine how the relevant components could be connected;
- identify technical constraints and open questions;
- prepare the information needed for the next implementation steps.

---

### Requirements
The following requirements need to be investigated and documented:

- **Visibility:** The LED panel must be clearly visible to a driver when entering the parking area.
- **Displayed information:** Define what information should be shown on the display, e.g. parking space number, licence plate number, and availability period.
- **Time periods:** Support different periods such as morning, afternoon, and full day.
- **Free spaces:** Define how availability should be displayed, e.g. “free until noon”.
- **Licence plates:** Consider different licence plate formats (Swiss, French, German, etc.) and define how they should be displayed.
- **Display limitations:** Check the maximum text/number length and whether the LED panel can display all required information.
- **Input/Output:** Define how information is sent to the LED panel and what input/output format is required.
- **Security:** Consider risks such as stolen hardware, unauthorized access, and possible network attacks.
- **Hardware protection:** Investigate whether additional physical protection.

---

### Criteria
The evaluation criteria should be sufficiently generic so that individual hardware or software components can be replaced without requiring a complete redesign of the solution.

The criteria should cover:
- **Visibility** — readability from the required distance and under expected lighting conditions.
- **Display capacity** — supported text length, number formats, brightness, etc.
- **Connectivity** — available communication interfaces and reliability.
- **Software support** — available libraries, compatibility, and maintainability.
- **Replaceability** — individual components should be replaceable without major changes to the overall architecture.
- **Compatibility** — compatibility with the existing hardware and Parkit system.
- **Scalability** — possibility to add or replace components later.
- **Security** — level of protection against unauthorized access and other relevant risks.
- **Cost** — initial cost, maintenance/replacement cost, and estimated cost over 10 years.

---

### Expected Outcome

- **Defined the architecture** — the overall LED integration architecture and how the main components interact.
- **Identified and acquired the required components** — the hardware and software required for the planned solution are known and available.
- **Implemented the LED integration** — the required components are connected and integrated into the Parkit system.

---

### Current Work

The work is currently focused on research and evaluation.

The work is divided into several areas:


| Area | Purpose |
|---|---|
| `led-basics/` | Understand LED matrix technology and identify suitable solutions |
| `existing-hardware/` | Identify available hardware and determine how it can be used |

These areas correspond to the research work being carried out in the project task tracker.

---

### Working Materials

The folders above contain the intermediate research, notes, diagrams and other materials produced during this work.

The materials are expected to evolve as the research progresses and may later be incorporated into the project's final technical documentation.
