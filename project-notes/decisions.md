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

---

New confirmed decisions should be added to this log when they are made.

---

## Pending Architecture Decisions

The following decisions must be made before selecting the final LED integration architecture.

| Topic | Decision Needed | Status | Related Work |
|---|---|---|---|
| Orchestrator | Which device should coordinate the LED system (Intel NUC, Raspberry Pi, or another option)? | Pending | [`LED Integration`](../workstream/led-integration/) |
| Communication | How should data be transmitted across the three parking levels (Ethernet, Wi-Fi, LoRa, or provider network)? | Pending | [`LED Integration`](../workstream/led-integration/) |
| LED Controller | Should we reuse the existing Pico W / Interstate 75 W setup or use a different controller? | Pending | [`LED Integration`](../workstream/led-integration/) |

---

New confirmed decisions should be added to the Decision Log when they are made.