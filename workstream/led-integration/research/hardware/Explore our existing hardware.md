# Explore Our Existing Hardware

| Date | 29.09.2026 |
|---|---|
| Project | P.A.R.K.I.T |
| Topic | Explore our existing hardware |

---

## Purpose

Identify the hardware currently available for the LED project, understand the basic role of each component, and determine how the components could potentially be connected.

---

## Hardware Overview

| Component | Hardware | Model | Role | Key Interface | Documentation |
|---|---|---|---|---|---|
| Display | RGB Matrix Panel | P3 2020 64×64-32s-m6 | Displays parking information | HUB75, 5V | [Device documentation](https://seengreat.com/wiki/74/rgb-matrix-p3-0-64x64) |
| Driver Board | Pimoroni Interstate 75 W | Interstate 75 W with Pico W | Connects the Pico W to the HUB75 LED panels and power | HUB75, GPIO | [Device guide](https://github.com/pimoroni/interstate75) · [Connection guide](https://learn.pimoroni.com/article/getting-started-with-interstate-75) |
| Microcontroller | Raspberry Pi Pico W | RP2040 | Controls the content displayed on the LED panels | GPIO, Wi-Fi, BLE | [Raspberry Pi documentation](https://www.raspberrypi.com/documentation/microcontrollers/pico-series.html) |
| Orchestrator | Intel NUC 13 Pro | Exact model to confirm | Originally planned to retrieve data from Parkit and distribute it to the display controllers | Ethernet, Wi-Fi, USB | [Intel NUC 13 Pro specification](https://download.intel.com/newsroom/2023/client-computing/Intel-NUC-13-Pro-Tech-Product-Spec.pdf) |

---

## Components

### RGB Matrix Panel

#### Description

The **P3 2020 64×64-32s-m6** is an indoor RGB LED matrix panel measuring approximately 192×192 mm.

Relevant specifications:

- 64×64 pixel resolution
- 3 mm pixel pitch
- HUB75 interface
- 1/32 scan rate
- 5V power supply
- 4,096 RGB LEDs

Two panels are currently planned to be used together as one display for a parking space.

#### Role

Displays parking information to drivers.

#### Connection

The panel uses the **HUB75 interface** and can be connected to the **Interstate 75 W** driver board.

---

### Interstate 75 W

#### Description

The **Pimoroni Interstate 75 W** is a controller/driver board designed for HUB75 RGB LED matrix panels.

The existing board includes a **Raspberry Pi Pico W**.

#### Role

Provides the interface between the Pico W, LED matrix panels, and power supply.

#### Connection

- Raspberry Pi Pico W → integrated with Interstate 75 W
- Interstate 75 W → HUB75 → RGB Matrix Panel

---

### Raspberry Pi Pico W

#### Description

The **Raspberry Pi Pico W** is a microcontroller based on the RP2040 chip with 2.4 GHz Wi-Fi, Bluetooth, and GPIO connectivity.

#### Role

Controls the content displayed on the LED panels.

In the existing setup, the Pico W is integrated into the Interstate 75 W.

---

### Intel NUC 13 Pro

#### Description

The **Intel NUC 13 Pro (Arena Canyon)** is a compact x86 computer.

The exact model of the available device should be confirmed.

#### Originally Planned Role

The Intel NUC was originally planned to act as the orchestrator:

- receive required data from Parkit;
- process/distribute the information;
- send the required information to the display controllers.

The final orchestrator architecture has not yet been selected.

---

## Possible Connection

A simplified view of how the existing hardware was originally expected to work:

```text
┌──────────────────────┐
│    Parkit / Server   │
└──────────┬───────────┘
           │
           │ Connection TBD
           ▼
┌──────────────────────┐
│    Intel NUC 13 Pro  │
│      Orchestrator    │
└──────────┬───────────┘
           │
           │ Connection TBD
           ▼
┌──────────────────────┐
│ Raspberry Pi Pico W  │
│ + Interstate 75 W    │
└──────────┬───────────┘
           │
           │ HUB75
           ▼
┌──────────────────────┐
│  2 × RGB LED Matrix  │
│        Panels        │
└──────────────────────┘
```

The communication method between the orchestrator and display controller is still under investigation.

---

## Open Questions

The main remaining questions related to the existing hardware are:

- How should the orchestrator communicate with the display controller?
- What cables, adapters, and power components are required?
- What software and libraries are required?
- Which existing components can be reused in the final architecture?

Detailed project questions are tracked in [`project-notes/open-questions.md`](../../../../project-notes/open-questions.md).

---

## Additional Estimate

### System Power Consumption & Annual Costs

The following estimate was prepared during the initial hardware research and is retained as working information. It represents a possible setup rather than the selected final architecture.

| System Component | Unit Power | Qty | Total Active Power | Annual Consumption | Estimated Annual Cost (0.334 CHF/kWh) |
|---|---:|---:|---:|---:|---:|
| Bay Logic & Displays (2× P3 RGB Matrix Panels + Interstate 75 W) | 25 W | 8 | 200 W | ~1,752 kWh | 585.17 CHF |
| Central Orchestrator (Intel NUC 13 Pro) | 25 W | 1 | 25 W | ~219 kWh | 73.15 CHF |
| System Total (including PSU efficiency overhead ~247 W) | — | — | ~247 W | ~2,167.6 kWh | 723.98 CHF |

> These values are preliminary estimates and should be reviewed as part of the architecture comparison.