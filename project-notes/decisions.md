# Project Decisions

This document records confirmed project decisions and their rationale.

Options still under research or discussion are not recorded as decisions.

---

## Decision Log
**ID format:** `DEC-XXX` — Project Decision

| ID | Decision | Rationale | Related Work |
|---|---|---|---|
| `DEC-001` | Facility Management approval is required before physical installation. | The installation affects the existing parking infrastructure, including mounting, cabling, and power. | [`Project Presentation`](../workstream/project-presentation/) |
| `DEC-002` | Requirements will have IDs, and related features and tests will be mapped to them. | This provides traceability between requirements, implementation, and testing. | [`LED Integration`](../workstream/led-integration/) |
| `DEC-003` | Architecture options will be researched before the hardware specialist review. | The team should understand the available options and prepare specific questions before getting technical feedback. | [`LED Integration`](../workstream/led-integration/) |
| `DEC-004` | LoRa / LoRaWAN will not be used for LED integration. | The team decided to pursue cellular communication instead. | [`LED Integration`](../workstream/led-integration/) |
| `DEC-005` | Mobile internet via SIM card will be used to connect the parking equipment to Parkit. | Parkit is cloud-hosted, so a direct Ethernet connection from the office is not required. | [`LED Integration`](../workstream/led-integration/) |
| `DEC-006` | LED displays must reflect reservation changes within a maximum of 1 minute. | Parking information must remain up to date. | [`LED Integration`](../workstream/led-integration/) |
| `DEC-007` | The LED system will use mains power instead of batteries. | The team agreed to use a wired power supply. | [`LED Integration`](../workstream/led-integration/) |
| `DEC-008` | Voltcraft ESP-3010 laboratory power supply (0–30 V DC, 0–10 A, 300 W) was purchased for LED hardware testing. | Provides adjustable power for testing the existing LED hardware. | [`LED Integration`](../workstream/led-integration/) |

---

New confirmed decisions should be added to this log when they are made.

---

## Pending Architecture Decisions

The following decisions must be made before selecting the final LED integration architecture.

| Topic | Decision Needed | Status | Related Work |
|---|---|---|---|
| Orchestrator | Which device should coordinate the LED system (Intel NUC, Raspberry Pi, or another option)? | Pending | [`LED Integration`](../workstream/led-integration/) |
| Local Communication | How should the Raspberry Pi 4 communicate with the LED controllers? | Pending | [`LED Integration`](../workstream/led-integration/) || LED Controller | Should we reuse the existing Pico W / Interstate 75 W setup or use a different controller? | Pending | [`LED Integration`](../workstream/led-integration/) |

---

New confirmed decisions should be added to the Decision Log when they are made.