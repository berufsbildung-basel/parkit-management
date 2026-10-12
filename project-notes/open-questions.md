# Open Questions

This document tracks unresolved questions that require research, clarification, or a decision.

Detailed research belongs in the relevant workstream. Resulting tasks are tracked on the Project Board.

---

## LED Matrix Integration

**Related work:** [`workstream/led-integration/`](../workstream/led-integration/)

### Architecture & Hardware

| Question | Status |
|---|---|
| Is the Intel NUC required as the orchestrator, or can a Raspberry Pi be used instead? | Open |
| Which of the three architecture options should be selected? | Open |
| Which existing hardware can be reused, and what additional components are required? | Open |
| What is the role of the Raspberry Pi Pico W / Interstate 75 W in the final architecture? | Open |
| How are the components connected in each architecture, including required cables and adapters? | Open |
| What power supplies are required for the controllers and LED panels? | Open |

### Software & Parkit Integration

| Question | Status |
|---|---|
| What changes are required in the existing Parkit application? | Open |
| What interface should be used between Parkit and the LED system? | Open |
| Which OS, software, drivers, and libraries are required for each architecture? | Open |
| How should the orchestrator communicate with the display controllers? | Open |

### Display

| Question | Status |
|---|---|
| What information must be displayed to the driver? | Open |
| Where should the information be displayed: at the entrance, at each parking space, or both? | Open |
| Are the existing two 64×64 LED panels per parking space sufficient for the required information? | Open |
| What viewing distance and lighting conditions must the display support? | Open |
| Can licence plate information be displayed, and are any privacy restrictions required? | Open |

### Communication & Installation

| Question | Status |
|---|---|
| Can Ethernet cables be installed to the required parking locations? | Open |
| Is LoRa suitable and reliable in the parking environment? | Open |
| If LoRa is used, how will the LoRa controller connect to the LED display? | Open |
| Where will the orchestrator, controllers, network equipment, and power supplies be installed? | Open |
| What power connections are available at the installation locations? | Open |

### LED Hardware Test

| Question | Status |
|---|---|
| Which exact cable/connector is required to connect and test the existing LED hardware? | Open |
| Is any additional hardware required for the test setup? | Open |
| Which software/library should be used to display a test message? | Open |

---

## Project Presentation & Administration Approval

**Related work:** [`workstream/project-presentation/`](../workstream/project-presentation/)

| Question | Status |
|---|---|
| What information and documentation does Facility Management require for approval? | Open |
| Are the proposed LED panel and equipment locations acceptable? | Open |
| What cable routing, power source, and mounting method are permitted? | Open |
| Are there building, electrical, or fire-safety requirements that affect the installation? | Open |

---

## Cost & Project Constraints

| Question | Status |
|---|---|
| What is the available project budget? | Open |
| What is the total estimated cost of each architecture, including installation? | Open |
| What are the expected electricity, maintenance, and replacement costs over 10 years? | Open |

---

## Expiring Reservation Reminder

**Related work:** [`workstream/reservation-reminder/`](../workstream/reservation-reminder/)

No open questions documented yet.