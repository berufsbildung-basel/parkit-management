# Open Questions

This document tracks unresolved questions that require research, clarification, or a decision.

Detailed research belongs in the relevant workstream. Resulting tasks are tracked on the Project Board.

The "Related Requirement" column references requirement IDs defined in the [LED Integration README](../workstream/led-integration/README.md).

---

## LED Matrix Integration

**Related work:** [`led-integration/`](../workstream/led-integration/)

### Architecture & Hardware

| Question | Related Requirement | Status |
|---|---|---|
| Should we use the existing Intel NUC or a Raspberry Pi as the orchestrator? | `INT-02`, `INT-03`, `INT-04` | Open |
| Which existing hardware can be reused, and what additional components are required? | `HW-01`, `HW-03` | Open |
| Can the existing Raspberry Pi Pico W / Interstate 75 W be reused in the proposed architectures? | `HW-01`, `HW-03` | Open |
| How are the components connected in each architecture, including required cables and adapters? | `HW-01` | Open |
| What power supplies are required for the controllers and LED panels? | `HW-01`, `HW-02` | Open |

### Software & Parkit Integration

| Question | Related Requirement | Status |
|---|---|---|
| What changes are required in the existing Parkit application? | `INT-03`, `INT-04` | Open |
| What interface should be used between Parkit and the LED system? | `INT-01`, `INT-02` | Open |
| Which OS, software, drivers, and libraries are required for each architecture? | — | Open |
| How should the orchestrator communicate with the display controllers? | `INT-02`, `REL-01`, `REL-02` | Open |

### Display

| Question | Related Requirement | Status |
|---|---|---|
| What exact information and format should be shown on the display? | `FR-01`, `FR-02`, `LP-03`, `DISP-02` | Open |
| Where should the information be displayed: at the entrance, at each parking space, or both? | `DISP-05` | Open |
| Are the existing two 64×64 LED panels per parking space sufficient for the required information? | `DISP-02`, `HW-01` | Open |
| What viewing distance and lighting conditions must the display support? | `DISP-01`, `DISP-03`, `DISP-05` | Open |
| What display format should be used for Swiss and foreign licence plates? | `LP-01`, `LP-02`, `LP-03` | Open |
| Are there any privacy restrictions on displaying licence plate information? | `LP-04` | Open |

### Communication & Installation

| Question | Related Requirement | Status |
|---|---|---|
| Which cellular router/modem and SIM plan should we use? | `HW-01`, `HW-05` | Open |
| Is mobile network coverage reliable in the parking area? | `HW-05`, `REL-01` | Open |
| How should the cellular router connect to the orchestrator and LED controllers? | `INT-02`, `HW-01` | Open |
| Where will the orchestrator, controllers, network equipment, and power supplies be installed? | `HW-01`, `HW-02` | Open |
| What power connections are available at the installation locations? | `HW-01`, `HW-02` | Open |

### LED Hardware Test

| Question | Related Requirement | Status |
|---|---|---|
| What exact connection, cable, and power components are required to test the existing LED hardware? | `HW-01` | Open |
| Is any additional hardware required for the test setup? | `HW-01` | Open |
| Which software/library should be used to display a test message? | — | Open |
| How can we display two different images on two separate LED panels? | `DISP-02`, `HW-01` | Open |

---

## Project Presentation & Administration Approval

**Related work:** [`project-presentation/`](../workstream/project-presentation/)

| Question | Related Requirement | Status |
|---|---|---|
| Are the proposed LED panel and equipment locations acceptable? | `DISP-05`, `HW-02` | Open |
| What cable routing, power source, and mounting method are permitted? | `HW-01`, `HW-02`, `HW-05` | Open |
| Are there building, electrical, or fire-safety requirements that affect the installation? | `HW-02` | Open |

---

## Cost & Project Constraints

| Question | Related Requirement | Status |
|---|---|---|
| What is the available project budget? | — | Open |
| What is the total estimated cost of each architecture, including installation? | — | Open |
| What are the expected electricity, maintenance, and replacement costs over 10 years? | — | Open |
| What will the mobile internet subscription and network equipment cost over 10 years? | — | Open |

---

## Expiring Reservation Reminder

**Related work:** [`reservation-reminder/`](../workstream/reservation-reminder/)

No open questions documented yet.