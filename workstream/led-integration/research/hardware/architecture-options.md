# LED Integration — Architecture Options

## Purpose

Compare the main architecture options for integrating the existing LED hardware with Parkit and provide a basis for architecture selection.

The current options are:

1. Intel NUC-based architecture
2. Raspberry Pi-based architecture
3. LoRa-based architecture

The Raspberry Pi option currently appears to be the most suitable direction, but no final architecture has been selected.

---

## Project Context

P.A.R.K.I.T is a parking reservation system for 8 parking spaces.

The LED integration should provide drivers with current parking information when entering the parking area.

### Main Use Cases

**UC-01 — Check Reserved Space**

A driver already has a reservation and uses the LED display to confirm which parking space is assigned.

**UC-02 — Find Free Space**

A driver sees that a parking space is currently free and then reserves it in Parkit.

### Environment

- 8 parking spaces
- 3 parking levels
- No existing Wi-Fi in the parking area
- 2 available power outlets
- Communication must work across all three parking levels
- Existing hardware should be reused where practical

---

## Key Requirements

| ID | Requirement |
|---|---|
| `FR-01` | Display the parking space assigned to a reservation. |
| `FR-02` | Show whether a parking space is currently available for reservation. |
| `FR-07` | Displayed parking availability must remain current. |
| `DISP-01` | Parking information must be clearly readable by drivers. |
| `INT-03` | LED-specific logic should remain separate from Parkit's core business logic. |
| `INT-05` | LED system failure must not prevent Parkit from operating normally. |
| `REL-04` | Outdated or incorrect parking information must not be displayed. |
| `HW-03` | Components should be replaceable without major changes to Parkit or the architecture. |
| `HW-05` | Communication must support equipment across all three parking levels. |

**TBD:** Required LED update frequency.

---

## Existing Hardware

| Component | Existing Hardware | Relevant Role |
|---|---|---|
| Display | P3 64×64 HUB75 RGB LED Matrix | Displays parking information |
| LED driver | Pimoroni Interstate 75 W | Connects the controller to the HUB75 panels |
| Microcontroller | Raspberry Pi Pico W | Controls the LED display |
| Computer | Intel NUC 13 Pro | Originally planned as the orchestrator |

Detailed hardware research: [`research/hardware/Explore our existing hardware.md`](research/hardware/Explore%20our%20existing%20hardware.md)

---

## Options Overview

| | Intel NUC | Raspberry Pi | LoRa |
|---|---|---|---|
| Main role | Orchestrator | Orchestrator / controller | Communication architecture |
| Existing LED panels | Reused | Reused | Reused if technically feasible |
| Existing Pico W / Interstate 75 W | Reused | Reused / to be evaluated | Reuse to be evaluated |
| Communication across parking levels | TBD | TBD | LoRa |
| Additional infrastructure | TBD | TBD | LoRa gateway or provider network |
| Main advantage | Existing planned setup | Simpler and lower-cost direction | No existing Wi-Fi required |
| Main concern | May be more hardware than required | Communication across 3 levels | Coverage, update frequency and LED integration |
| Current direction | Alternative | **Preferred direction** | Alternative |

---

## Option 1 — Intel NUC as Orchestrator

### Architecture

```text
Parkit / Server
      │
      │ Connection TBD
      ▼
Intel NUC 13 Pro
   Orchestrator
      │
      │ Communication TBD
      ▼
Pico W + Interstate 75 W ×8
      │
      │ HUB75
      ▼
Existing RGB LED Panels
2 panels per parking space
```

### Components & Connections

| Component | Role | Connection |
|---|---|---|
| Intel NUC 13 Pro | Orchestrator | Ethernet / Wi-Fi available; final connection TBD |
| Pico W + Interstate 75 W | LED controller | Communication with NUC TBD |
| RGB LED Matrix | Display | HUB75 |
| Power supply | Powers controllers and displays | Exact setup TBD |

### Software

| Component | Possible Software | Status |
|---|---|---|
| Intel NUC | Linux | TBD |
| NUC → controllers | MQTT | Possible option |
| Pico W / Interstate 75 W | Pimoroni software/libraries | To verify |

### Main Advantages

- Reuses the existing Intel NUC.
- Reuses the existing Pico W / Interstate 75 W and LED panels.
- Standard Linux environment.

### Main Limitations / Open Points

- The NUC may provide more computing power than the project requires.
- Communication between the NUC and controllers across the three parking levels is not defined.
- Additional network infrastructure may be required.
- Required cables, power setup, and installation effort are still TBD.

### Cost

TBD — include additional hardware, infrastructure, installation, electricity, and estimated 10-year cost.

---

## Option 2 — Raspberry Pi as Orchestrator

### Architecture

```text
Parkit / Server
      │
      │ Connection TBD
      ▼
Raspberry Pi
   Orchestrator
      │
      │ Communication TBD
      ▼
Pico W + Interstate 75 W ×8
      │
      │ HUB75
      ▼
Existing RGB LED Panels
2 panels per parking space
```

### Components & Connections

| Component | Role | Connection |
|---|---|---|
| Raspberry Pi | Orchestrator | Ethernet / Wi-Fi available; final connection TBD |
| Pico W + Interstate 75 W | LED controller | Communication with Raspberry Pi TBD |
| RGB LED Matrix | Display | HUB75 |
| Power supply | Powers controllers and displays | Exact setup TBD |

### Software

| Component | Possible Software | Status |
|---|---|---|
| Raspberry Pi | Linux | TBD |
| Raspberry Pi → controllers | MQTT | Possible option |
| Pico W / Interstate 75 W | Pimoroni software/libraries | To verify |

### Main Advantages

- Lower hardware and power requirements than the Intel NUC.
- Reuses the existing Pico W / Interstate 75 W and LED panels.
- Standard Linux environment.
- Raspberry Pi appears sufficient for the expected orchestration tasks.

### Main Limitations / Open Points

- Communication across the three parking levels is not defined.
- There is no existing Wi-Fi in the parking area.
- Additional network infrastructure may be required.
- Required cables, power setup, and installation effort are still TBD.
- Raspberry Pi suitability for the expected request volume and update frequency must be confirmed.

### Cost

TBD — include Raspberry Pi, additional infrastructure, installation, electricity, and estimated 10-year cost.

### Current Assessment

This is currently the preferred direction, but the architecture has not yet been selected.

---

## Option 3 — LoRa-Based Communication

### Architecture

Two LoRa approaches are currently being considered:

#### Option 3A — Private LoRa

```text
Parkit / Server
      │
      ▼
Private LoRa Gateway
      │
      │ LoRa
      ▼
LoRa-capable Controller ×8
      │
      │ Connection TBD
      ▼
Existing RGB LED Panels
```

#### Option 3B — Provider LoRaWAN

```text
Parkit / Server
      │
      │ Internet
      ▼
LoRaWAN Provider Network
      │
      │ LoRa
      ▼
LoRa-capable Controller ×8
      │
      │ Connection TBD
      ▼
Existing RGB LED Panels
```

### Components & Connections

| Component | Role | Connection |
|---|---|---|
| LoRa gateway / provider network | Communication between Parkit and parking equipment | LoRa / LoRaWAN |
| LoRa-capable controller | Receives parking information | LoRa |
| Existing LED setup | Displays parking information | HUB75 |
| Additional interface | Connects LoRa controller to existing LED setup | TBD |
| Power supply | Powers controllers and displays | Exact setup TBD |

### Software

| Component | Possible Software | Status |
|---|---|---|
| Private LoRa gateway | LoRaWAN network server, e.g. ChirpStack | Possible option |
| LoRa controller | LoRa communication library | TBD |
| Controller → LED | Display library / interface | TBD |
| Provider LoRaWAN | Provider integration | To investigate |

### Main Advantages

- Does not require existing Wi-Fi across the parking levels.
- May reduce the need for data cabling between parking levels.
- Designed for small amounts of wireless data over longer distances.

### Main Limitations / Open Points

- LoRa coverage across the three parking levels must be validated.
- Suitability for the required LED update frequency must be confirmed.
- Integration with the existing Pico W / Interstate 75 W / HUB75 setup is not yet defined.
- Additional controller or interface hardware may be required.
- Private LoRa requires local gateway infrastructure.
- Provider LoRaWAN introduces an external service dependency and recurring costs.

### Cost

TBD — compare:

- gateway and LoRa hardware;
- controller/interface hardware;
- provider subscription where applicable;
- installation;
- electricity;
- estimated 10-year cost.

### Current Assessment

LoRa remains an alternative communication approach.

Its suitability depends mainly on coverage, required update frequency, and whether the existing LED hardware can be reused without unnecessary complexity.

---

## Architecture Comparison

| Criterion | Intel NUC | Raspberry Pi | LoRa-Based |
|---|---|---|---|
| Existing LED panels | Reused | Reused | Reuse to be confirmed |
| Existing Pico W / Interstate 75 W | Reused | Reused | Reuse to be confirmed |
| Communication across 3 parking levels | TBD | TBD | LoRa / LoRaWAN |
| Existing Wi-Fi required | Depends on final connection | Depends on final connection | No |
| Additional infrastructure | TBD | TBD | Gateway or provider network |
| Parkit integration | TBD | TBD | TBD |
| Update frequency support | To validate | To validate | To validate |
| Reliability in parking environment | To validate | To validate | LoRa coverage must be tested |
| Hardware complexity | TBD | TBD | Additional LoRa hardware/interface may be required |
| Replaceability | To evaluate | To evaluate | To evaluate |
| Installation effort | TBD | TBD | TBD |
| Initial cost | TBD | TBD | TBD |
| Running cost | TBD | TBD | Provider option may include recurring fees |
| 10-year cost | TBD | TBD | TBD |
| Main open point | Is the NUC necessary? | How should controllers be connected across the 3 levels? | Can LoRa meet update needs and reuse the existing LED setup? |
| Current direction | Alternative | **Preferred direction** | Alternative |

---

## Cost Comparison

Costs are preliminary and will be updated once the required components and installation setup are confirmed.

| Cost Area | Intel NUC | Raspberry Pi | LoRa-Based |
|---|---|---|---|
| Main computer / orchestrator | Existing hardware | ~60–135 CHF | Not necessarily required |
| LED panels | Existing hardware | Existing hardware | Existing hardware if reusable |
| Pico W / Interstate 75 W | Existing hardware | Existing hardware | Reuse to be confirmed |
| Communication hardware | TBD | TBD | Gateway / LoRa hardware required |
| Cabling / network infrastructure | TBD | TBD | Potentially reduced |
| Installation | TBD | TBD | TBD |
| Recurring connectivity cost | None identified | None identified | Provider option may require subscription |
| Electricity | To calculate | To calculate | To calculate |
| Estimated 10-year cost | TBD | TBD | TBD |

### Cost Notes

- Existing hardware should be reused where practical.
- Installation and cabling may represent a significant part of the total cost.
- Private LoRa and provider-based LoRa must be calculated separately.
- Final 10-year estimates should include hardware, installation, electricity, connectivity, maintenance, and expected replacement costs.

---

## Current Direction

Based on the current research, the Raspberry Pi architecture appears to be the most suitable direction.

Main reasons:

- Lower hardware and power requirements than the Intel NUC.
- Can reuse the existing Pico W / Interstate 75 W and LED panels.
- Provides enough flexibility for the expected orchestration tasks.
- Avoids using the Intel NUC if its additional computing power is not required.

No final architecture has been selected yet.

The main remaining question is how to provide reliable communication across the three parking levels.

---

## Questions for Hardware Expert

- Is Raspberry Pi suitable as the main orchestrator for this system?
- What is the best way to connect the equipment across the three parking levels without existing Wi-Fi?
- Is the Intel NUC necessary, or is Raspberry Pi sufficient?
- Is LoRa a reasonable option for this use case?
- Can LoRa be integrated while keeping the existing Pico W / Interstate 75 W / HUB75 LED setup?
- Can the communication method support the required LED update frequency?
- What hardware, cables, connectors, and power components are required for the existing LED hardware test?
- What should we validate in a Proof of Concept before selecting the final architecture?