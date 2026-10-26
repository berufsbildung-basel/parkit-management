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
| Should we use Raspberry Pi 4 or 5 for the final system? | `HW-01`, `HW-04` | Open |
| Which existing hardware can be reused, and what additional components are required? | `HW-01`, `HW-03` | Open |
| Can the existing Raspberry Pi Pico W / Interstate 75 W be reused in the proposed architectures? | `HW-01`, `HW-03` | Open |
| How are the components connected in each architecture, including required cables and adapters? | `HW-01` | Open |
| What power supplies are required for the controllers and LED panels? | `HW-01`, `HW-02` | Open |
| Should we use a microSD card or SSD for the Raspberry Pi 4/5? | `HW-06` | Open |
| Can one Raspberry Pi control all 8 parking spaces, and how many LED controllers are needed? | `HW-03`, `HW-04` | Open |
| How should we distribute power from the two available outlets to all 16 LED panels and their controllers? | `HW-01`, `HW-02` | Open |
| Can each Interstate 75 W share a 5 V power supply with its two LED panels, and what power capacity is required? | `HW-01`, `HW-02` | Open |

### Software & Parkit Integration

| Question | Related Requirement | Status |
|---|---|---|
| What changes are required in the existing Parkit application? | `INT-03`, `INT-04` | Open |
| Which OS, software, drivers, and libraries are required for each architecture? | — | Open |
| How should the orchestrator communicate with the display controllers? | `INT-02`, `REL-01`, `REL-02` | Open |
| Can the existing Parkit API provide the current status of all 8 parking spaces? | `INT-01`, `FR-03` | Open |
| How will Raspberry Pi authenticate with the Parkit API? | `INT-02`, `SEC-01` | Open |
| What commands should Raspberry Pi send to the LED controllers via USB? | `INT-02` | Open |
| How will Raspberry Pi access the Parkit API securely? | `INT-02`, `SEC-01`, `SEC-03` | Open |
| What polling interval is needed to update LED displays within 1 minute? | `FR-04` | Open |

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
| Which 4G router and SIM plan should we use (e.g. Wingo)? | `HW-07`, `HW-08` | Open |
| How much mobile data will the system use per month? | `HW-09` | Open |
| Is mobile network coverage reliable in the parking area? | `HW-05`, `REL-01` | Open |
| How should the cellular router connect to the orchestrator and LED controllers? | `INT-02`, `HW-01` | Open |
| Where will the orchestrator, controllers, network equipment, and power supplies be installed? | `HW-01`, `HW-02` | Open |
| What power connections are available at the installation locations? | `HW-01`, `HW-02` | Open |
| Which 4G router and SIM plan should we use (e.g. Wingo)? | `HW-01`, `HW-05` | Open |

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

### Local Communication

| Question | Related Requirement | Status |
|---|---|---|
| How should Raspberry Pi communicate with the LED controllers across all 8 parking spaces (Wi-Fi or wired connection)? | `INT-02`, `HW-01`, `REL-01` | Open |

### Power Distribution

| Question | Related Requirement | Status |
|---|---|---|
| How can we safely power 16 LED panels and their controllers using the two available power outlets? | `HW-01`, `HW-02` | Open |

---


## Expiring Reservation Reminder

**Related work:** [`reservation-reminder/`](../workstream/reservation-reminder/)

No open questions documented yet.