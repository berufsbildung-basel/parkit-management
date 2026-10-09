# Posible solutions

## Contents

- Overview
- Possible structure
	- Solution 1: Cable + Raspberry Pi
	- Solution 2: Cable + Intel NUC
	- Solution 3: LoRa gateway + orchestrator with LoRa HAT
	- Solution 4: LoRa gateway + microcontroller with native LoRa
	- Solution 5: Swisscom LoRaWAN
	- Overview (for Possible structure)
- Components
    - Orchestrator
        - Table of options
        - Pros and cons
    - Microcontroller
        - Table of options
        - Pros and cons
    - Display
        - Table of options
        - Pros and cons
    - Type of Connection 1
        - Table of options
        - Pros and cons
    - Type of Connection 2
        - Table of options
        - Pros and cons

## Overview

This document outlines the proposed architectural structure for the project and evaluates the technical components required for its implementation. It serves as a comprehensive reference to guide the selection of hardware, software, and communication interfaces.

The following structure serves as the baseline architecture from which all system variations are derived:

`Server ➔ [Type of Connection 1] ➔ Orchestrator ➔ [Type of Connection 2] ➔ Microcontroller ➔ Display`

#### Possible structure

##### Solution 1: Cable + Raspberry Pi

```
Server ➔ Physical cable (Ethernet) ➔ Raspberry Pi 4/5 ➔ Wi-Fi (MQTT) ➔ Raspberry Pi Pico W + Interstate 75 W  ➔ RGB P3 Matrix Panel 64x64, 2 panels per place
```

- Simplest setup with the most reliable data link (wired), native fit with HUB75 panels (Pico W + Interstate 75 W).
- Needs a Wi-Fi access point in the garage and the cable laying.

##### Solution 2: LoRa gateway + microcontroller with native LoRa

```
Server ➔ Indoor LoRaWAN Gateway ➔ LoRa ➔ MCU with Native LoRa, e.g. ESP32-S3 LoRa ➔ E-Ink Color Display 7.3" Spectra 6
```

- No orchestrator and no Wi-Fi needed.
- Best suited for ePaper: LED panels are hard to connect to LoRa boards (see Microcontroller cons).
- The gateway must be placed next to the server.

##### Solution 3: Swisscom LoRaWAN

```
Server ➔ Internet (HTTPS) ➔ Swisscom LPN LoRaWAN ➔ LoRa ➔ MCU with Native LoRa, e.g. ESP32-S3 LoRa  ➔ E-Ink Color Display 7.3" Spectra 6
```

- No own gateway to buy or maintain, only the LPN subscription (~5.40 – 42.00 CHF/year).
- Signal coverage in the underground garage must be tested first.

##### Overview (for Possible structure)

|#|Server|Connection 1|Orchestrator|Connection 2|Microcontroller|Display|
|---|---|---|---|---|---|---|
|1|Server|Physical cable|Raspberry Pi 4/5|Wi-Fi (MQTT)|Raspberry Pi Pico W + Interstate 75 W|RGB P3 Matrix Panel 64x64 (2× per place)|
|2|Server|LoRaWAN Gateway|–|LoRa|MCU with Native LoRa (e.g. ESP32-S3 LoRa)|E-Ink Color Display 7.3" Spectra 6|
|3|Server|Swisscom LPN|–|LoRa|MCU with Native LoRa (e.g. ESP32-S3 LoRa)|E-Ink Color Display 7.3" Spectra 6|

##### Cost and risk comparison (8 parking spaces)

Prices are estimates based on the component tables. The Interstate 75 W board, power supplies, enclosures and the Wi-Fi access point are not included.

| #   | Setup                                                          | Total price (hardware + installation)                                                        | Electricity per year (approx.)                            | Risks and difficulties                                                                                                                                                                                                                                                     |
| --- | -------------------------------------------------------------- | -------------------------------------------------------------------------------------------- | --------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1   | Cable + Raspberry Pi + Pico W + RGB P3 Matrix Panel 64x64 (2×) | **~1'900 – 3'600 CHF** (Pi 60–135, cable 1'200–2'800, 8× Pico W 48–64, 8× panels (2×) ~576)  | **~390 CHF** (Pi 14.56 + 8× [Pico W 0.58 + panels 46.60]) | Core drilling through three concrete fire barriers; highest installation cost; LED panels dominate the running cost; Wi-Fi coverage in the garage needed; microSD corruption on power loss (UPS recommended); open PCBs need an enclosure                                  |
| 2   | LoRa gateway + MCU with LoRa + E-Ink 7.3" Spectra 6            | **~870 – 1'370 CHF** (gateway 70–250, 8× MCU 80–160, 8× ePaper ~720–960)                     | **~25 CHF** (gateway 11.65 + 8× [MCU 1.46 + ePaper 0.20]) | LoRa coverage in the garage must be tested; airtime limits (868 MHz) allow only short messages; ePaper is slow (~12 s refresh), small (800×480) and hard to read in the dark without a lamp; custom wiring and code for the MCU; gateway must be placed next to the server |
| 3   | Swisscom LoRaWAN + MCU with LoRa + E-Ink 7.3" Spectra 6        | **~800 – 1'120 CHF** (8× MCU 80–160, 8× ePaper ~720–960) + LPN subscription 5.40–42 CHF/year | **~13 CHF** (8× [MCU 1.46 + ePaper 0.20])                 | Public network may not penetrate the underground concrete (possible dead zones); recurring subscription (if billed per node, up to ~340 CHF/year for 8 nodes, to be clarified); dependency on Swisscom; same airtime, ePaper and custom-code limits as Solution 2          |
## Components
### Orchestrator 

#### Table of options:

| Type    | Component Name                                  | Hardware Price (Est.) | Average Power Draw  | Connectivity               | Compatibility                                                          | Replaceability / Scalability                                                    | Exact 1-Year Electricity Cost |
| ------- | ----------------------------------------------- | --------------------- | ------------------- | -------------------------- | ---------------------------------------------------------------------- | ------------------------------------------------------------------------------- | ----------------------------- |
| Mini PC | **Intel NUC**  <br>(Intel/ASUS NUC)             | 350.00 – 650.00 CHF   | ~10 W (idle 5–15 W) | Ethernet, Wi-Fi, USB       | **Native:** Runs standard x86 Parkit backend binaries out-of-the-box.  | **High / Limited:** Easily hot-swapped, but physical port counts limit scaling. | **29.13CHF**                  |
|         | **Raspberry Pi 4 / 5** <br>                     | 60.00 – 135.00 CHF    | **5 W**             | Ethernet, Wi-Fi, GPIO, USB | **High:** Linux-based. Can run local script parsing and queue routing. | **High / Max:** Multi-display routing via single script orchestration.          | **14.56 CHF**                 |
| MCU     |                                                 |                       |                     |                            |                                                                        |                                                                                 |                               |
#### Pros and cons:

**Intel NUC**

- **Pros:**
	- **Zero Code Modification:** Runs enterprise x86 binaries natively without cross-compilation delays.
	- **Reliable Storage**: NVMe SSDs are far more durable than microSD cards; a UPS is still recommended against sudden power loss
	- **Offline Heavy Autonomy:** Vast processing headroom to host local booking backups if main servers crash.
	- **Active Internal Cooling:** Factory fan assembly prevents hardware thermal throttling under heavy room temperatures.
- **Cons:**
	- **High Financial Footprint:** Highest initial hardware cost (up to 650 CHF) and annual power overhead (72.82 CHF).
	- **Sealed Cabinet Risk:** Generates 25W of continuous heat; cannot be locked inside tight, unventilated electrical boxes.
	- **No Native GPIO Pins:** Requires extra external USB-to-Serial converter boxes to talk to raw hardware components.

**Raspberry Pi 4 / 5**

- **Pros:**
	- **Cost-Efficient Queueing:** Great balance of low hardware cost (60–135 CHF) and minimal power draw (14.56 CHF/year).
	- **Direct Hardware Pins:** Exposed physical GPIO layout connects directly to industrial transceivers without USB adapters.
	- **Massive Automation Libraries:** Complete Linux OS support for standard Python/Node.js display distribution scripts.
- **Cons:**
	- **MicroSD Storage Fragility:** Standard memory cards wear down fast and corrupt easily during abrupt power outages.
	- **Hidden Accessory Cost:** Requires separate purchases of industrial cases, heatsinks, and specialized power regulators for production.

---

### Microcontroller

#### Table of options:

| Component Name                                      | Hardware Price (Est.) | Average Power Draw     | Connectivity           | Compatibility                                                         | Replaceability / Scalability                                                      | Exact 1-Year Electricity Cost |
| --------------------------------------------------- | --------------------- | ---------------------- | ---------------------- | --------------------------------------------------------------------- | --------------------------------------------------------------------------------- | ----------------------------- |
| **Raspberry Pi Pico W**  <br>(Microcontroller chip) | 6.00 – 8.00 CHF       | **0.2 W**              | Wi-Fi, BLE, GPIO       | **Maximum:** 100% native fit with Pimoroni Interstate 75 W footprint. | **Maximum:** Mass-market board, hot-swappable in seconds.                         | **0.58 CHF**                  |
| **MCU with Native LoRa**  <br>(e.g., ESP32-S3 LoRa) | 10.00 – 20.00 CHF     | **0.5 W**              | LoRa, Wi-Fi, BLE, GPIO | **Medium:** Requires custom wiring; breaks Interstate 75 footprint.   | **Medium:** Readily available on the market, but relies on custom code templates. | **1.46 CHF**                  |
| **Built-in MCU**  <br>(All-in-one Smart Display)    | Included in panel     | **1.5 W** (Logic only) | RS-485, Ethernet       | **Low:** Bound to proprietary closed-source manufacturer SDKs.        | **Low:** Monolithic setup; cannot change the processor core.                      | **4.37 CHF**                  |

#### Pros and cons:

**Raspberry Pi Pico W**

- **Pros:**
	- **Glitch-Free Video Driving:** Features dedicated PIO (Programmable I/O) hardware state machines to drive HUB75 matrix panels flawlessly without CPU lag.
	- **Native Shield Ecosystem:** Direct physical drop-in compatibility with the Pimoroni Interstate 75 W, lowering production soldering time.
	- **Ultra-Low Electrical Overhead:** Costs under 0.60 CHF per year in continuous 24/7 background operation.
- **Cons:**
	- **No On-Board Battery Logic:** Lacks native battery charging/management circuitry, requiring external power distribution boards.
	- **Highly Constrained RAM:** Limited volatile memory prevents processing heavy visual content or full video streaming.

**MCU with Native LoRa (e.g., ESP32-S3 LoRa)**

- **Pros:**
	- **Single-Chip Wireless Link:** Combines processing logic and long-range sub-GHz radio reception onto one board without auxiliary modules.
	- **Dual-Core Processing Core:** Massive clock speed headroom to parse radio data in the background while updating screen text.
	- **Built-In Power Regulators:** Typically features integrated lithium-polymer battery connectors and charging chips directly on-board.
- **Cons:**
	    - **LED Connection Difficulties:** Lack of off-the-shelf breakout boards on the market combining LoRa and HUB75 makes physical integration with the LED panel highly challenging.
	- **Software Rewrite Needed:** Driving HUB75 panels on alternative MCUs requires entirely different libraries, forcing a complete overhaul of your display code.

**Built-in MCU (All-in-one Smart Display)**

- **Pros:**
	- **Commercial Clean Aesthetics:** Factory-sealed industrial presentation with zero loose component wires or external development enclosures.
	- **Hardened Power Input:** built-in voltage regulation circuitry ensures stable operation—even with poor-quality power or voltage fluctuations—without the need for external adapters
	- **Lower Assembly Time:** Arrives pre-built and pre-wired from the vendor, eliminating field bench assembly labor.
- **Cons:**
	- **Complete Vendor Lock-In:** Software features, security patches, and network protocols are entirely dependent on the manufacturer's updates.
	- **Monolithic Hardware Failure:** If a single component on the micro-controller fails, the entire visual display panel must be discarded and replaced.




---


#### Display

##### Table of options:

|Type|Component Name|Hardware Price (Est.)|Average Power Draw|Connectivity|Compatibility|Replaceability / Scalability|Exact 1-Year Electricity Cost|
|---|---|---|---|---|---|---|---|
|LED Matrix (HUB75)|**1. [RGB P3 Matrix Panel 64x64 (2x)](https://www.waveshare.com/rgb-matrix-p3-64x64.htm)**|~72 CHF per place|**16 W**  <br>(2 panels, max. 40 W)|HUB75, separate 5 V supply per panel|**Maximum:** Native fit with Pimoroni Interstate 75 W + Pico W.|**High:** Standard HUB75 panels from many vendors, chainable.|**46.60 CHF**|
|ePaper / E-Ink|**2. [E-Ink Color Display 7.3" Spectra 6](https://core-electronics.com.au/7-3inch-6-color-e-paper-display-e-ink-hat.html)**|~90–120 CHF per place|**0.07 W**  <br>(max. during refresh, standby ≈ 0)|SPI (driver HAT, 3.3 V / 5 V)|**High:** Works with Pico W / ESP32 / Raspberry Pi, Waveshare provides SPI demo code.|**Medium:** Waveshare-specific panel.|**0.20 CHF**|
||**3. [ePaper 10.3" (IT8951 HAT)](https://www.robotshop.com/products/waveshare-103-e-paper-e-ink-display-hat-for-raspberry-pi-18721404-black-white-16-grey-scales-usb-spi-i80)**|~158 CHF per place|**0.1 W**  <br>(Standby; 1.2 W only during refresh)|USB / SPI / I80 via IT8951 driver HAT|**Medium:** HAT is built for the Raspberry Pi 40-pin header. Pico W possible via SPI wiring, but needs custom code.|**Medium:** Waveshare-specific panel and driver board.|**0.29 CHF**|
|LCD (HDMI)|**4. [LCD HDMI 13–16"](https://www.galaxus.ch/de/search?q=15.6%20zoll%20hdmi%20monitor)** (e.g. 15.6" monitor, search link)|~130–250 CHF per place (without Pi)|**12 W** (without Pi)|HDMI + power supply|**Low–Medium:** Needs a Raspberry Pi (or similar SBC) per place. A Pico W cannot drive HDMI.|**High:** Standard monitor with VESA mount, available everywhere.|**34.95 CHF** (without Pi)|

##### Pros and cons:

**1. RGB P3 Matrix Panel 64x64 (2x)**

- **Pros:**
    - **Excellent Visibility:** Self-illuminating and very bright, readable when driving in and in a dark garage.
    - **Signal Colors:** Green/red status can be seen from far away.
    - **Native Pico W Fit:** Drop-in with the Interstate 75 W, low assembly effort.
- **Cons:**
    - **Limited Text Space:** Pixel limit makes long names or license plate formats tight.
    - **High Power Draw:** About 47 CHF per year per place, much higher than the ePaper options.
    - **Low Hardware Protection:** Open PCB, needs an acrylic or IP54 enclosure in the garage.
    - **Hard to Combine with LoRa:** No off-the-shelf boards combine LoRa and HUB75, so it fits only the Wi-Fi/Pico W setup.

**2. E-Ink Color Display 7.3" Spectra 6**

- **Pros:**
    - **Low Price:** Cheapest e-paper option with color.
    - **Pico W / ESP32 Compatible:** SPI interface, no SBC needed.
    - **Almost No Power:** About 0.20 CHF per year.
- **Cons:**
    - **Slow Refresh:** About 12 s according to Waveshare.
    - **Small Area:** 800×480 pixels, only large text for name, plate and time.
    - **Not Self-Illuminating:** Hard to read in a dark garage without a lamp.
    - **Fragile:** Needs protective glass or an enclosure against impact.

**3. ePaper 10.3" (IT8951 HAT)**

- **Pros:**
    - **Very Low Power:** Only the refresh uses energy, the image stays without power.
    - **Fast Refresh:** Full refresh under 1 s according to Waveshare, partial refresh supported.
    - **Good Text Capacity:** 1872×1404 pixels, name, license plate (CH/DE/FR) and time fit well.
- **Cons:**
    - **Poor Distance Readability:** Not self-illuminating, hard to read from a distance in a dark garage without an extra lamp.
    - **No Signal Colors:** Black/white only.
    - **More Integration Work:** Built for the Raspberry Pi header, so an ESP32 needs custom SPI wiring and code.
    - **Fragile:** Needs protective glass against impact.

**4. LCD HDMI 13–16"**

- **Pros:**
    - **Maximum Flexibility:** Unlimited text, logos and special characters.
    - **Excellent Readability:** Large text, readable even while driving past.
    - **Robust Housing:** Many models come with metal frames and VESA mounts.
- **Cons:**
    - **Extra SBC Per Place:** Each display needs its own Raspberry Pi, which adds cost and maintenance.
    - **High Running Cost:** 12 W continuous, about 35 CHF per year per place, plus about 15 CHF per year for the Raspberry Pi.
    - **Cabling:** Power and HDMI have to be routed to every place.
    - **Not Compatible with LoRa Setups:** Needs a Raspberry Pi per place, so it only fits a Wi-Fi-based structure.

**Summary**

- **Best Visibility:** Option 1 (P3 Matrix): very bright and readable from far away, but high power draw.
- **Lowest Running Cost:** Option 2 (E-Ink Spectra 6): almost no power and the cheapest ePaper per place, but slow and hard to read in the dark.
- **Most Text Space (ePaper):** Option 3 (ePaper 10.3"): fast refresh and a lot of space, but black/white only and more integration work.
- **Maximum Flexibility:** Option 4 (LCD 13–16"): easiest to design, but needs a Raspberry Pi per place and has high running cost.
### Type of Connection 1

#### Table of options:


| Type           | Component Name                                                                                                           | Hardware Price (Est.)                                | Average Power Draw | Connectivity                              | Compatibility                                                                                                  | Replaceability / Scalability                                                                                                                   | Exact 1-Year Electricity Cost |
| -------------- | ------------------------------------------------------------------------------------------------------------------------ | ---------------------------------------------------- | ------------------ | ----------------------------------------- | -------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------- |
| LoRaWAN        | **Indoor LoRaWAN Gateway** (one Indoor LoRaWAN Gateway must be placed next to the server)                                | 70.00 – 250.00 CHF                                   | 4 W                | RS-485 Serial Bus, Ethernet               | **Native Server Ecosystem:** Runs internal LoRaWAN stacks (e.g., ChirpStack).                                  | **High:** Fully integrated industrial-grade chassis with standardized protocols.                                                               | 11.65 CHF                     |
|                | **LoRa HAT** (for a single-board computer / orchestrator) (one Indoor LoRaWAN Gateway must be placed next to the server) | 90–130 CHF                                           | 0.1 W – 0.5 W      | SPI / UART                                | **Hardware Module:** Requires a compatible 40-pin header on the single-board computer.                         | **Maximum:** Detachable board. Can be easily replaced or swapped onto a different host computer.                                               | 0.29 – 1.46 CHF               |
|                | **Swisscom LPN LoRaWAN**                                                                                                 | Requires an LPN subscription: ~5.40 – 42.00 CHF/year | –                  | LoRaWAN via public Swisscom base stations | **Cloud Webhook Integration:** Swisscom Network Server relays data directly to your Parkit API via HTTPS POST. | **Maximum:** No physical gateway hardware to manage; instant scaling over the air.                                                             | –                             |
| Physical Cable | Physical Cable Laying                                                                                                    | 1'200.00 – 2'800.00 CHF                              | –                  | RJ45                                      | **Universal Standard:** Instantly compatible with all standard routers, switches, and NUC/Pi setups.           | **Low / Fixed:** Physical wires are fixed in conduits and hard to re-route, but they can handle future bandwidth upgrades without replacement. | –                             |
#### Pros and cons:

**Indoor LoRaWAN Gateway**

- **Pros:**
    - **Local Control:** Runs localized network stacks (e.g., ChirpStack), keeping data processing completely within the facility boundary.
    - **Industrial Housing:** Standardized factory enclosures protect the radio core from building dust and power drops.
- **Cons:**
    - **Initial Hardware Footprint:** Requires buying and securing a dedicated physical router unit near the server room.
    - **Data Rate Caps:** Constrained by regional 868 MHz airtime regulations, limiting updates to short text packs.

**LoRa HAT** (for Single Board Computer)

- **Pros:**
    - **Lowest Core Cost:** The cheapest physical hardware option (25.00 – 40.00 CHF) to add long-range radio features to an existing setup.
    - **Direct Host Swapping:** Plugs into standard 40-pin computer rails, making component replacement fast and simple.
- **Cons:**
    - **Host Thermal Throttling Risk:** Mounting the expansion shield directly over the host computer's main processor blocks airflow, leading to high thermal risks inside tight electrical enclosures.
    - **Hardware Resource Conflicts:** Occupying the SPI and GPIO bus lanes for the LoRa link often locks out the physical ability to simultaneously attach other industrial hats (such as hardware RS-485 shields).

**Swisscom LPN LoRaWAN**

- **Pros:**
    - **Zero Local Hardware Setup:** Bypasses buying, mounting, or maintaining private radio routers on the facility floor.
    - **Direct Web Integration:** Relays garage data straight to your Parkit API endpoint via encrypted cloud webhooks .
- **Cons:**
    - **Underground Penetration Failure:** Public telecom waves often struggle to penetrate thick basement concrete, risking dead zones.
    - **Continuous Opex Fees:** Replaces upfront installation capital with rolling multi-year contract subscription costs per node.

**Physical Cable Laying**

- **Pros:**
    - **Infinite Data Flow:** No network packet limits or wireless lag; moves heavy logging or debug files seamlessly.
    - **Zero Interference Shadows:** Completely unaffected by moving vehicles, heavy garage doors, or basement concrete structures.
- **Cons:**
    - **Severe Structural Labor:** Demands structural core drilling across three concrete floor fire barriers and layout positioning inside vertical technical risers.
    - **Highest Upfront Capital:** Initial deployment costs are significantly higher.


---

### Type of Connection 2

#### Table of options:

*(noch offen)*

#### Pros and cons:

*(noch offen)*
