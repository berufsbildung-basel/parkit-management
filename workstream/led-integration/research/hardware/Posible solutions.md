
### Contents

- Overview
- Possible structure
    - Solution 1: Cable + Raspberry Pi + LED panels
    - Solution 2: LoRa gateway + microcontroller with native LoRa
    - Solution 3: Swisscom LoRaWAN
    - Solution 4: Cable + Raspberry Pi + LCD
    - Solution 5: Cable + Raspberry Pi + ePaper 10.3"
    - Overview (for Possible structure)
    - Cost and risk comparison
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

### Overview

This document outlines the proposed architectural structure for the project and evaluates the technical components required for its implementation. It serves as a comprehensive reference to guide the selection of hardware, software, and communication interfaces.

The following structure serves as the baseline architecture from which all system variations are derived:

`Server ➔ [Type of Connection 1] ➔ Orchestrator ➔ [Type of Connection 2] ➔ Microcontroller ➔ Display`

### Possible structure

Legend: `(×8)` = one unit per parking space.

#### Solution 1: Cable + Raspberry Pi + LED panels

```
Server ➔ Cat6 Ethernet cable ➔ Raspberry Pi 5 (4 GB) ➔ Wi-Fi (MQTT) ➔ Pimoroni Interstate 75 W with Raspberry Pi Pico W (×8) ➔ Waveshare RGB-Matrix-P3-64x64, 2 panels per place (×8)
```

- Reliable wired data link
- Native fit: Pico W + Interstate 75 W + HUB75
- Needs Wi-Fi access point and cable laying

#### Solution 2: LoRa gateway + microcontroller with native LoRa

```
Server ➔ RAK7268V2 WisGate Edge Lite 2 (EU868) ➔ LoRa 868 MHz ➔ Heltec WiFi LoRa 32 V3 (×8) ➔ Waveshare 7.3inch e-Paper HAT (E), 800×480, Spectra 6 (×8)
```

- No orchestrator, no Wi-Fi
- ePaper fits best (LED panels hard to connect to LoRa boards)
- Gateway next to the server

#### Solution 3: Swisscom LoRaWAN

```
Server ➔ Internet (HTTPS) ➔ Swisscom LPN LoRaWAN ➔ LoRa 868 MHz ➔ Heltec WiFi LoRa 32 V3 (×8) ➔ Waveshare 7.3inch e-Paper HAT (E), 800×480, Spectra 6 (×8)
```

- No own gateway, only LPN subscription (~5.40 – 42.00 CHF/year)
- Garage coverage must be tested first

#### Solution 4: Cable + Raspberry Pi + LCD

```
Server ➔ Cat6 Ethernet cable ➔ Raspberry Pi 5 (4 GB) ➔ Wi-Fi (MQTT) ➔ Raspberry Pi Zero 2 W (×8) ➔ 15.6" HDMI monitor (×8)
```

- Most flexible layout (text, logos)
- Pi Zero 2 W, power and HDMI cable per place
- Needs Wi-Fi access point and cable laying

#### Solution 5: Cable + Raspberry Pi + ePaper 10.3"

```
Server ➔ Cat6 Ethernet cable ➔ Raspberry Pi 5 (4 GB) ➔ Wi-Fi (MQTT) ➔ Raspberry Pi Zero 2 W (×8) ➔ Waveshare 10.3inch e-Paper HAT (IT8951), 1872×1404 (×8)
```

- IT8951 HAT fits the Pi Zero 2 W header
- Most text space of the ePaper options, fast refresh, black/white only
- Needs Wi-Fi access point and cable laying

#### Overview (for Possible structure)

|#|Server|Connection 1|Orchestrator|Connection 2|Microcontroller / Controller|Display|
|---|---|---|---|---|---|---|
|1|Server|Cat6 Ethernet cable|Raspberry Pi 5 (4 GB)|Wi-Fi (MQTT)|Pimoroni Interstate 75 W with Raspberry Pi Pico W|Waveshare RGB-Matrix-P3-64x64 (2× per place)|
|2|Server|RAK7268V2 WisGate Edge Lite 2 (EU868)|–|LoRa 868 MHz|Heltec WiFi LoRa 32 V3|Waveshare 7.3inch e-Paper HAT (E)|
|3|Server|Swisscom LPN LoRaWAN|–|LoRa 868 MHz|Heltec WiFi LoRa 32 V3|Waveshare 7.3inch e-Paper HAT (E)|
|4|Server|Cat6 Ethernet cable|Raspberry Pi 5 (4 GB)|Wi-Fi (MQTT)|Raspberry Pi Zero 2 W|15.6" HDMI monitor|
|5|Server|Cat6 Ethernet cable|Raspberry Pi 5 (4 GB)|Wi-Fi (MQTT)|Raspberry Pi Zero 2 W|Waveshare 10.3inch e-Paper HAT (IT8951)|

#### Cost and risk comparison (8 parking spaces)

Estimates based on the component tables. Not included: Interstate 75 W board, power supplies, enclosures, Wi-Fi access point. Pi Zero 2 W: ~15–20 CHF, ~1 W (~2.91 CHF/year).

| #   | Setup                                                           | Total price (hardware + installation)                                                                  | Electricity per year (approx.)                               | Risks and difficulties                                                                                                                                                                                                  |
| --- | --------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1   | Cable + Raspberry Pi + Pico W + RGB P3 Matrix Panel 64x64 (2×)  | **~1'900 – 3'600 CHF** (Pi 60–135, cable 1'200–2'800, 8× Pico W 48–64, 8× panels (2×) ~576)            | **~390 CHF** (Pi 14.56 + 8× [Pico W 0.58 + panels 46.60])    | - Core drilling through 3 fire barriers  <br>- LED panels dominate running cost  <br>- Wi-Fi in garage needed  <br>- microSD corruption (UPS)  <br>- Open PCBs need enclosure                                           |
| 2   | LoRa gateway + MCU with LoRa + E-Ink 7.3" Spectra 6             | **~870 – 1'370 CHF** (gateway 70–250, 8× MCU 80–160, 8× ePaper ~720–960)                               | **~25 CHF** (gateway 11.65 + 8× [MCU 1.46 + ePaper 0.20])    | - LoRa coverage must be tested  <br>- 868 MHz airtime limits: short messages only  <br>- ePaper slow (~12 s), small, dark in garage  <br>- Custom wiring and code  <br>- Gateway next to server                         |
| 3   | Swisscom LoRaWAN + MCU with LoRa + E-Ink 7.3" Spectra 6         | **~800 – 1'120 CHF** (8× MCU 80–160, 8× ePaper ~720–960) + LPN subscription 5.40–42 CHF/year           | **~13 CHF** (8× [MCU 1.46 + ePaper 0.20])                    | - Possible dead zones underground  <br>- Subscription (per node up to ~340 CHF/year, to be clarified)  <br>- Dependency on Swisscom  <br>- Same airtime, ePaper and code limits as Solution 2                           |
| 4   | Cable + Raspberry Pi 5 + 8× Pi Zero 2 W + 15.6" HDMI monitor    | **~2'400 – 5'100 CHF** (Pi 60–135, cable 1'200–2'800, 8× Pi Zero 2 W ~120–160, 8× monitor 1'040–2'000) | **~320 CHF** (Pi 14.56 + 8× [Pi Zero ~2.91 + monitor 34.95]) | - Most expensive setup  <br>- 16 devices with microSD (corruption)  <br>- Power and HDMI cable per place  <br>- Core drilling through 3 fire barriers  <br>- Wi-Fi in garage needed  <br>- Bulky monitors need mounting |
| 5   | Cable + Raspberry Pi 5 + 8× Pi Zero 2 W + ePaper 10.3" (IT8951) | **~2'650 – 4'400 CHF** (Pi 60–135, cable 1'200–2'800, 8× Pi Zero 2 W ~120–160, 8× ePaper ~1'264)       | **~40 CHF** (Pi 14.56 + 8× [Pi Zero ~2.91 + ePaper 0.29])    | - High cable cost  <br>- microSD per place (corruption)  <br>- Black/white only, no signal color  <br>- Hard to read in the dark  <br>- Needs protective glass  <br>- Wi-Fi in garage needed                            |

### Components

#### Orchestrator

##### Table of options:

|Type|Component Name|Hardware Price (Est.)|Average Power Draw|Connectivity|Compatibility|Replaceability / Scalability|Exact 1-Year Electricity Cost|
|---|---|---|---|---|---|---|---|
|Mini PC|**Intel NUC**  <br>(Intel/ASUS NUC)|350.00 – 650.00 CHF|~10 W (idle 5–15 W)|Ethernet, Wi-Fi, USB|**Native:** Runs standard x86 Parkit backend binaries out-of-the-box.|**High / Limited:** Easily hot-swapped, but physical port counts limit scaling.|**29.13CHF**|
||**Raspberry Pi 4 / 5**|60.00 – 135.00 CHF|**5 W**|Ethernet, Wi-Fi, GPIO, USB|**High:** Linux-based. Can run local script parsing and queue routing.|**High / Max:** Multi-display routing via single script orchestration.|**14.56 CHF**|
|MCU||||||||

##### Pros and cons:

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

#### Microcontroller

##### Table of options:

|Component Name|Hardware Price (Est.)|Average Power Draw|Connectivity|Compatibility|Replaceability / Scalability|Exact 1-Year Electricity Cost|
|---|---|---|---|---|---|---|
|**Raspberry Pi Pico W**  <br>(Microcontroller chip)|6.00 – 8.00 CHF|**0.2 W**|Wi-Fi, BLE, GPIO|**Maximum:** 100% native fit with Pimoroni Interstate 75 W footprint.|**Maximum:** Mass-market board, hot-swappable in seconds.|**0.58 CHF**|
|**MCU with Native LoRa**  <br>(e.g., ESP32-S3 LoRa)|10.00 – 20.00 CHF|**0.5 W**|LoRa, Wi-Fi, BLE, GPIO|**Medium:** Requires custom wiring; breaks Interstate 75 footprint.|**Medium:** Readily available on the market, but relies on custom code templates.|**1.46 CHF**|
|**Built-in MCU**  <br>(All-in-one Smart Display)|Included in panel|**1.5 W** (Logic only)|RS-485, Ethernet|**Low:** Bound to proprietary closed-source manufacturer SDKs.|**Low:** Monolithic setup; cannot change the processor core.|**4.37 CHF**|

##### Pros and cons:

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
    - **Complete Vendor Lock-In:** Software features, security patches, and network protocols are entirely dependent on the manufacturer’s updates.
    - **Monolithic Hardware Failure:** If a single component on the micro-controller fails, the entire visual display panel must be discarded and replaced.

---

#### Display

##### Table of options:

|Type|Component Name|Hardware Price (Est.)|Average Power Draw|Connectivity|Compatibility|Replaceability / Scalability|Exact 1-Year Electricity Cost|
|---|---|---|---|---|---|---|---|
|LED Matrix (HUB75)|**1. [RGB P3 Matrix Panel 64x64 (2x)](https://www.waveshare.com/rgb-matrix-p3-64x64.htm)**|~72 CHF per place|**16 W**  <br>(2 panels, max. 40 W)|HUB75, 5 V supply per panel|**Maximum:** Native fit with Interstate 75 W + Pico W|**High:** Standard panels, chainable|**46.60 CHF**|
|ePaper / E-Ink|**2. [E-Ink Color Display 7.3" Spectra 6](https://core-electronics.com.au/7-3inch-6-color-e-paper-display-e-ink-hat.html)**|~90–120 CHF per place|**0.07 W**  <br>(max. during refresh, standby ≈ 0)|SPI (3.3 V / 5 V)|**High:** Pico W / ESP32 / Raspberry Pi, SPI demo code|**Medium:** Waveshare-specific|**0.20 CHF**|
||**3. [ePaper 10.3" (IT8951 HAT)](https://www.robotshop.com/products/waveshare-103-e-paper-e-ink-display-hat-for-raspberry-pi-18721404-black-white-16-grey-scales-usb-spi-i80)**|~158 CHF per place|**0.1 W**  <br>(standby; 1.2 W during refresh)|USB / SPI / I80 via IT8951|**Medium:** Built for Raspberry Pi header, Pico W needs custom code|**Medium:** Waveshare-specific|**0.29 CHF**|
|LCD (HDMI)|**4. [LCD HDMI 13–16"](https://www.galaxus.ch/de/search?q=15.6%20zoll%20hdmi%20monitor)** (e.g. 15.6" monitor, search link)|~130–250 CHF per place (without Pi)|**12 W** (without Pi)|HDMI + power supply|**Low–Medium:** Needs Raspberry Pi per place|**High:** Standard monitor, VESA mount|**34.95 CHF** (without Pi)|

##### Pros and cons:

**1. RGB P3 Matrix Panel 64x64 (2x)**

- **Pros:**
    - Very bright, readable in dark garage
    - Green/red status visible from far away
    - Drop-in with Interstate 75 W
- **Cons:**
    - Little text space
    - ~47 CHF/year per place
    - Open PCB, needs enclosure (acrylic / IP54)
    - Only fits Wi-Fi/Pico W setup (no LoRa boards with HUB75)

**2. E-Ink Color Display 7.3" Spectra 6**

- **Pros:**
    - Cheapest color ePaper
    - SPI, works with Pico W / ESP32, no extra computer needed
    - ~0.20 CHF/year
- **Cons:**
    - Slow refresh (~12 s)
    - Small (800×480), only large text
    - Not self-illuminating, hard to read in the dark
    - Fragile, needs protective glass or enclosure

**3. ePaper 10.3" (IT8951 HAT)**

- **Pros:**
    - Very low power, image stays without power
    - Fast refresh (under 1 s), partial refresh possible
    - Lots of text space (1872×1404)
- **Cons:**
    - Not self-illuminating, hard to read from far away in the dark
    - Black/white only
    - Built for Raspberry Pi header, ESP32 needs custom SPI wiring and code
    - Fragile, needs protective glass

**4. LCD HDMI 13–16"**

- **Pros:**
    - Unlimited text, logos, special characters
    - Large and readable, even when driving past
    - Robust housing, VESA mount
- **Cons:**
    - Own Raspberry Pi per place (extra cost and maintenance)
    - 12 W continuous, ~35 CHF/year per place + ~15 CHF/year for the Pi
    - Power and HDMI cable to every place
    - Not compatible with LoRa setups

**Summary**

- **Best visibility:** Option 1 (P3 Matrix), but high power draw
- **Lowest running cost:** Option 2 (E-Ink Spectra 6), but slow and dark
- **Most text space (ePaper):** Option 3 (10.3"), but black/white and more integration work
- **Most flexible:** Option 4 (LCD), but needs a Raspberry Pi per place and high running cost

---

#### Type of Connection 1

##### Table of options:

|Type|Component Name|Hardware Price (Est.)|Average Power Draw|Connectivity|Compatibility|Replaceability / Scalability|Exact 1-Year Electricity Cost|
|---|---|---|---|---|---|---|---|
|LoRaWAN|**Indoor LoRaWAN Gateway** (one Indoor LoRaWAN Gateway must be placed next to the server)|70.00 – 250.00 CHF|4 W|RS-485 Serial Bus, Ethernet|**Native Server Ecosystem:** Runs internal LoRaWAN stacks (e.g., ChirpStack).|**High:** Fully integrated industrial-grade chassis with standardized protocols.|11.65 CHF|
||**LoRa HAT** (for a single-board computer / orchestrator) (one Indoor LoRaWAN Gateway must be placed next to the server)|90–130 CHF|0.1 W – 0.5 W|SPI / UART|**Hardware Module:** Requires a compatible 40-pin header on the single-board computer.|**Maximum:** Detachable board. Can be easily replaced or swapped onto a different host computer.|0.29 – 1.46 CHF|
||**Swisscom LPN LoRaWAN**|Requires an LPN subscription: ~5.40 – 42.00 CHF/year|–|LoRaWAN via public Swisscom base stations|**Cloud Webhook Integration:** Swisscom Network Server relays data directly to your Parkit API via HTTPS POST.|**Maximum:** No physical gateway hardware to manage; instant scaling over the air.|–|
|Physical Cable|Physical Cable Laying|1'200.00 – 2'800.00 CHF|–|RJ45|**Universal Standard:** Instantly compatible with all standard routers, switches, and NUC/Pi setups.|**Low / Fixed:** Physical wires are fixed in conduits and hard to re-route, but they can handle future bandwidth upgrades without replacement.|–|

##### Pros and cons:

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
    - **Host Thermal Throttling Risk:** Mounting the expansion shield directly over the host computer’s main processor blocks airflow, leading to high thermal risks inside tight electrical enclosures.
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

#### Type of Connection 2

##### Table of options:

_(noch offen)_

##### Pros and cons:

_(noch offen)_



### My recommendation

Option?