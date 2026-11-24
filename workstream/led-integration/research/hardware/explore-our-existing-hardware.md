# Explore Our Existing Hardware

## Contents

1. [Purpose](#purpose)
2. [Hardware Overview](#hardware-overview)
3. [Roles](#roles)
<!-- 4. [Open Questions](#open-questions)-->


## Purpose

Identify the hardware currently available for the LED project, understand the basic role of each component, and determine how the components could potentially be connected.



## Hardware Overview
 

| Role | Qty | Item | Source | Price | Status |
|---|---:|---|---|---|---|
| Display | 4 | P5 tile 64x32, 320 x 160 mm, with ribbon and power cable | AliExpress, item 1005011661208809 | EUR 147.13 total incl. shipping | In the office since 24.11.2026 (Ordered 10 November 2026) |
| Display | 1 | RGB Matrix Panel P3 2020 64×64-32s-m6, 192 x 192 mm | In hand | - | - |
| Display | 1 | RGB Matrix Panel P4 2020 64×32-16s, 256 x 128 mm | In hand | - | - |
| Driver board / microcontroller | 1 | Pimoroni Interstate 75 W, RP2350A (PIM727) | BerryBase.ch | CHF 22.90 | In the office since 18.11.2026 (ordered 10.11.2026) |
| Driver board / microcontroller | 5 | Interstate 75 W with Pico W (RP2040) | In hand | - | - |
| Data wiring | 4 | HUB75 ribbon cable, short | In hand | - | - |
| Data wiring | 1 | HUB75 ribbon cable, long | In hand | - | - |
| Power wiring | 1 | Test lead 1 mm², 2 x 4 mm banana plug, 50 cm, red (T1325526) | BerryBase.ch | CHF 1.65 | In the office since 18.11.2026 (ordered 10.11.2026) |
| Power wiring | 1 | Test lead 1 mm², 2 x 4 mm banana plug, 50 cm, black (T1325525) | BerryBase.ch | CHF 1.65 | In the office since 18.11.2026 (ordered 10.11.2026) |
| Power wiring | 4 | Wago 221-415 connector, 5-way (2 needed, 2 spare) | BerryBase.ch | from CHF 0.75 each | In the office since 18.11.2026 (ordered 10.11.2026) |
| Power supply | 1 | Voltcraft ESP-3010 lab supply | In hand (DEC-008) | - | - |
| Orchestrator | 1 | Intel NUC 13 Pro (exact model to confirm) | In hand | - | - |
| Orchestrator | 1 | Raspberry Pi 4B | In hand | - | - |

 




## Roles
 
### Display
 
The display shows the parking status to drivers, mounted above each parking space.
 
Several panel types are available so they can be compared before a final choice is made:
 
- **P5 64×32 tiles** — 4 tiles are combined into one 2×2 display unit.
- **P3 64×64 and P4 64×32 panels** — kept for comparison of size, pixel pitch, and readability.
### Driver board / microcontroller
 
LED matrix panels cannot be connected directly to a computer. They are controlled through the HUB75 interface, which requires a fast, precisely timed signal. The driver board generates this signal and runs the code that decides what is shown on the panels. Its Wi-Fi connection allows it to receive status updates.
 
Two versions are available for comparison:
 
- **Interstate 75 W with Pico W (RP2040)** — the existing board.
- **Interstate 75 W (RP2350A, PIM727)** — the newer version, with more memory and processing power.
### Orchestrator
 
The orchestrator is the central device that retrieves parking data from Parkit and distributes it to the display controllers. This way, each display controller does not need its own connection to Parkit.
 
The Intel NUC 13 Pro was originally planned for this role. The final orchestrator architecture has not yet been selected.
 
### Power supply
 
The LED panels require 5 V at several amps. During bench testing, the Voltcraft ESP-3010 lab supply is used because the voltage can be set exactly to 5.0 V and the current can be limited, which protects the panels in case of a wiring mistake.
 
The lab supply is intended for testing only, not for the final installation.
 
### Power wiring
 
The power wiring connects the lab supply to the panels:
 
- **Test leads (red/black, 4 mm banana plugs)** — connect the outputs of the lab supply to the power input.
- **Wago 221-415 connectors** — distribute the 5 V from one supply output to several panels.

<!--
## Open Questions

The main remaining questions related to the existing hardware are:

- How should the orchestrator communicate with the display controller?
- What cables, adapters, and power components are required?
- What software and libraries are required?
- Which existing components can be reused in the final architecture?

Detailed project questions are tracked in [`project-notes/open-questions.md`](../../../../project-notes/open-questions.md).
-->
