### Contents

- Overview
- Possible structure
    - Architecture 1: Intel NUC + Interstate 75 W + HUB75 LED matrix
    - Architecture 2: Raspberry Pi 5 + Interstate 75 W + HUB75 LED matrix
    - Architecture 3: Private LoRaWAN + Seeed XIAO ESP32S3 / Wio-SX1262 + ePaper
    - Overall comparison
    - Open points
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
- Recommendation

### Overview

This document outlines the proposed architectural structure for the project and evaluates the technical components required for its implementation. It serves as a comprehensive reference to guide the selection of hardware, software, and communication interfaces.

The following structure serves as the baseline architecture from which all system variations are derived:

`Server ➔ [Type of Connection 1] ➔ Orchestrator(not necessarily) ➔ [Type of Connection 2] ➔ Microcontroller ➔ Display`

---

### Possible structure

This section evaluates three possible architectures for integrating the Parkit application with the parking displays. Each architecture is evaluated using the same project requirements and evaluation criteria.

**Architecture options**

1. Intel NUC Orchestrator + Wi-Fi/MQTT + Interstate 75 W (Pico W) Controllers + HUB75 LED Matrix
2. Raspberry Pi 5 Orchestrator (Ethernet or LoRa uplink) + Wi-Fi/MQTT + Interstate 75 W (Pico W) Controllers + HUB75 LED Matrix
3. Private LoRaWAN Gateway + Seeed XIAO ESP32S3 / Wio-SX1262 Controllers + ePaper Displays

---

#### Architecture 1 — Intel NUC Orchestrator + Interstate 75 W Controllers + HUB75 LED Matrix

##### 1. Architecture Diagram

<img src="workstream/led-integration/research/hardware/imgg/Pasted image 20261012102657.png" width=400 heigth= auto>
##### 2. Components

| Component                | Qty. | Role                                                                                        |
| ------------------------ | ---- | ------------------------------------------------------------------------------------------- |
| Server                   | 1    | Python-based Parkit API integration (HTTPS)                                                 |
| Intel NUC                | 1    | Orchestrator: receives Parkit data, runs the MQTT broker and routes data to the controllers |
| Interstate 75 W + Pico W | 8    | MCU: receives MQTT messages and drives the LED panel                                        |
| LED Matrix Panels        | 8    | Displays parking information                                                                |

##### 3. Software & Libraries

|Component|Software|Libraries|
|---|---|---|
|Server|Python 3, API integration (HTTPS)|`requests`, `paho-mqtt`|
|Intel NUC|Linux (e.g. Ubuntu), Mosquitto broker|Python 3, `requests`, `paho-mqtt`|
|Interstate 75 W + Pico W|Pimoroni MicroPython firmware|`interstate75`, `hub75`, `picographics`, `umqtt.simple`|
|LED Matrix Panels|—|Driven directly by the MCU's `hub75` / `interstate75` libraries — no separate display library needed|

##### 4. Advantages / Disadvantages

**Advantages**

- Stable wired link between server and orchestrator.
- NUC provides high performance and reliable storage.
- Only one Ethernet cable run (server → NUC); no per-display cabling.
- MQTT decouples the orchestrator from the display controllers.
- HUB75 panels are driven directly by the MCU — no separate display controller board or library.
- Display controllers can be replaced independently.

**Disadvantages**

- Highest orchestrator cost.
- Requires Wi-Fi coverage at every display location in the garage.
- Wi-Fi access point(s) are not part of the current setup and must be added.
- 8 MCUs must be maintained (firmware, Wi-Fi credentials, MQTT configuration).
- MQTT broker and Wi-Fi security must be defined.

##### 5. Requirements & Criteria

|Area|Assessment|Notes|
|---|---|---|
|Parkit integration|Good|Server/orchestrator separates Parkit from display hardware|
|Replaceability|Good|Controllers and displays are separated via MQTT|
|Connectivity|To validate|Wired to the NUC, but Wi-Fi coverage in the garage must be tested|
|Reliability|Good / To validate|Reliable orchestrator; depends on Wi-Fi quality at the displays|
|Software support|Good|Linux, Python and MicroPython ecosystems|
|Scalability|Good|Additional controllers can subscribe to the broker|
|Security|TBD|MQTT authentication/TLS and Wi-Fi security must be defined|
|Visibility|TBD|Physical test required|
|Display capacity|TBD|Physical test required; panel type and size to be confirmed|
|Cost|High|NUC + access point(s) + 8 controllers + panels|

---

#### Architecture 2 — Raspberry Pi 5 Orchestrator + Interstate 75 W Controllers + HUB75 LED Matrix

##### 1. Architecture Diagram
<img src="workstream/led-integration/research/hardware/imgg/Pasted image 20261012100345.png" width=400, heigth=auto>
 
##### 2. Components

| Component                | Qty. | Role                                                                                        |
| ------------------------ | ---- | ------------------------------------------------------------------------------------------- |
| Server                   | 1    | Parkit API integration                                                                      |
| Raspberry Pi 5           | 1    | Orchestrator: receives Parkit data, runs the MQTT broker and routes data to the controllers |
| LoRa HAT (SPI/UART)      | 1    | Hardware add-on — required for Option B only                                                |
| Interstate 75 W + Pico W | 8    | MCU: receives MQTT messages and drives the LED panel                                        |
| LED Matrix Panels        | 8    | Displays parking information                                                                |

##### 3. Software & Libraries

|Component|Software|Libraries|
|---|---|---|
|Server|—|—|
|Raspberry Pi 5|Raspberry Pi OS, Mosquitto broker, ChirpStack (only if using LoRa HAT)|Python 3, `requests`, `paho-mqtt`|
|Interstate 75 W + Pico W|Pimoroni MicroPython firmware|`interstate75`, `hub75`, `picographics`, `umqtt.simple`|
|LED Matrix Panels|—|Driven directly by the MCU's `hub75` / `interstate75` libraries — no separate display library needed|

##### 4. Advantages / Disadvantages

**Advantages**

- Lower cost than Intel NUC.
- Low power consumption.
- Linux and broad software/library support.
- Two uplink options: Ethernet (Option A) or LoRa (Option B) — flexible if no cable run is available.
- MQTT decouples the orchestrator from the display controllers.
- HUB75 panels are driven directly by the MCU — no separate display library.

**Disadvantages**

- microSD reliability must be considered.
- Case, cooling and a suitable power supply are required.
- Requires Wi-Fi coverage at every display location; access point(s) must be added.
- Option B needs an additional LoRa HAT and ChirpStack, which increases complexity.
- Option B: the LoRa path from the server to the orchestrator is not fully defined yet (see Open points).
- 9 devices must be maintained (1 Pi + 8 MCUs).

##### 5. Requirements & Criteria

|Area|Assessment|Notes|
|---|---|---|
|Parkit integration|Good|Integration can remain separate from LED logic|
|Replaceability|Good|Standard Linux/MQTT architecture; orchestrator can be swapped|
|Connectivity|To validate|Option A wired; Wi-Fi coverage (and LoRa coverage for Option B) must be tested|
|Reliability|Good / Medium|Pi storage (microSD) requires consideration; depends on Wi-Fi quality|
|Software support|Good|Linux, Python and MicroPython ecosystems|
|Scalability|Good|Additional controllers can subscribe to the broker|
|Security|TBD|MQTT authentication/TLS and Wi-Fi security must be defined|
|Visibility|TBD|Physical test required|
|Display capacity|TBD|Physical test required; panel type and size to be confirmed|
|Cost|Medium|Cheaper orchestrator than NUC; LoRa HAT adds cost for Option B|

---

#### Architecture 3 — Private LoRaWAN Gateway + Seeed XIAO ESP32S3 / Wio-SX1262 Controllers + ePaper Displays

##### 1. Architecture Diagram

<img src="workstream/led-integration/research/hardware/imgg/architecture-3-lorawan-epaper.png" width=400, heigth=auto>

##### 2. Components

|Component|Qty.|Role|
|---|---|---|
|Server|1|Python-based Parkit API integration (HTTPS)|
|RAK7268V2 (WisGate Edge Lite 2)|1|LoRaWAN gateway: connects the server side to the LoRa devices|
|Seeed XIAO ESP32S3 + Wio-SX1262|8|MCU: receives parking data via LoRaWAN (868 MHz) and controls the display|
|ePaper Display 7.3" Spectra 6|8|Displays parking information|

##### 3. Software & Libraries

|Component|Software|Libraries|
|---|---|---|
|Server|Python 3, API integration (HTTPS)|`requests`|
|RAK7268V2|ChirpStack network server|—|
|Seeed XIAO ESP32S3 + Wio-SX1262|Arduino core for ESP32 (PlatformIO)|`RadioLib` (SX1262 LoRaWAN), `ArduinoJson`, `GxEPD2`|
|ePaper Display 7.3" Spectra 6|—|`GxEPD2` (`GxEPD2_730c_GDEP073E01`), `Adafruit_GFX`|

##### 4. Advantages / Disadvantages

**Advantages**

- No Ethernet cable required at every parking space.
- No Wi-Fi required.
- One gateway can communicate with multiple controllers.
- Low controller power consumption.
- ePaper only consumes power when the image changes.
- Display connects to the MCU via SPI; ESP32-S3 with Arduino/MicroPython support and 11 GPIOs.

**Disadvantages**

- LoRa coverage in the garage must be tested.
- Low bandwidth.
- Additional LoRaWAN software/infrastructure (ChirpStack).
- ePaper has a slow refresh rate; suitability for frequently changing status must be tested.
- ePaper is not self-illuminated; visibility in the garage depends on ambient lighting.
- Pushing updates to battery-optimised LoRaWAN nodes needs a defined downlink strategy (device class / polling interval).
- 868 MHz duty-cycle limits apply to uplinks.
- Embedded firmware (C++/Arduino) must be developed and maintained for 8 MCUs.
- The ePaper HAT must be wired to the XIAO headers by hand; the board has only one SPI interface, which the LoRa module likely shares (pin assignment to be checked).

##### 5. Requirements & Criteria

|Area|Assessment|Notes|
|---|---|---|
|Parkit integration|Good|Gateway/network server can isolate Parkit from hardware|
|Replaceability|Medium / Good|Standard LoRaWAN helps, but display integration is hardware-specific|
|Connectivity|To validate|Garage coverage test required|
|Reliability|To validate|Depends on LoRa coverage|
|Software support|Medium|Additional embedded/LoRaWAN stack required|
|Scalability|Good|One gateway can support multiple nodes|
|Security|Good / TBD|LoRaWAN provides security mechanisms; implementation must be defined|
|Visibility|TBD|ePaper readability in garage lighting must be tested|
|Display capacity|TBD|7.3" display; content/refresh behaviour to be validated|
|Cost|Low / Medium|Less cabling, but gateway and LoRa controllers required|

---

#### Overall Comparison

|Criterion|1 — Intel NUC + Wi-Fi/MQTT|2 — Raspberry Pi 5 + Wi-Fi/MQTT|3 — Private LoRaWAN + ePaper|
|---|---|---|---|
|Integration effort|Medium|Medium (higher with Option B)|High|
|Replaceability|Good|Good|Medium / Good|
|Connectivity|To validate (Wi-Fi)|To validate (Wi-Fi, LoRa for Option B)|To validate (LoRa)|
|Reliability|Good / To validate|Good / Medium|To validate|
|Software support|Good|Good|Medium|
|Display technology|HUB75 LED matrix|HUB75 LED matrix|ePaper 7.3" Spectra 6|
|Display capacity|TBD|TBD|TBD|
|Scalability|Good|Good|Good|
|Installation effort|Low / Medium|Low / Medium|Low / Medium|
|Security|TBD|TBD|TBD|
|Cost|High|Medium|Low / Medium|
|Main risk|Cost / Wi-Fi coverage|Storage / Wi-Fi coverage / LoRa path (Option B)|LoRa coverage + ePaper visibility and refresh|

---

#### Open Points

The following points must be validated before selecting the final architecture:

- Wi-Fi coverage in the parking garage and required access points (Architectures 1 and 2).
- LoRa coverage in the parking garage (Architecture 3 and Architecture 2 / Option B).
- Architecture 2 / Option B: define how the server reaches the Pi over LoRa (gateway placement, LoRa HAT role, ChirpStack setup).
- Which LED matrix panel (size, pitch, resolution) will be used with the Interstate 75 W.
- Communication protocol and message format between Parkit, orchestrator and controllers (MQTT topics, payload, LoRaWAN downlink/device class).
- ePaper refresh time, readability and visibility in the garage lighting.
- Display readability and capacity.
- Security approach (MQTT authentication/TLS, Wi-Fi security, LoRaWAN key management).
- Installation cost, including power supply for each display.
- Total 10-year cost.

---

### Components

#### Orchestrator

##### Table of options:

|Type|Component Name|Hardware Price (Est.)|Average Power Draw|Connectivity|Compatibility|Replaceability / Scalability|Exact 1-Year Electricity Cost|
|---|---|---|---|---|---|---|---|
|Mini PC|**Intel NUC** <br>(Intel/ASUS NUC)|350.00 – 650.00 CHF|~10 W (idle 5–15 W)|Ethernet, Wi-Fi, USB|**Native:** Runs standard x86 Parkit backend binaries out-of-the-box.|**High / Limited:** Easily hot-swapped, but physical port counts limit scaling.|**29.13 - 72.82 CHF**|
||**Raspberry Pi 4 / 5**|60.00 – 135.00 CHF|**5 W**|Ethernet, Wi-Fi, GPIO, USB|**High:** Linux-based. Can run local script parsing and queue routing.|**High / Max:** Multi-display routing via single script orchestration.|**14.56 CHF**|

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

|Type|Component Name|Hardware Price (Est.)|Average Power Draw|Connectivity|Compatibility|Replaceability / Scalability|Exact 1-Year Electricity Cost|
|---|---|---|---|---|---|---|---|
|MCU|**Raspberry Pi Pico W** <br>(Microcontroller chip)|6.00 – 8.00 CHF|**0.2 W**|Wi-Fi, BLE, GPIO|**Maximum:** 100% native fit with Pimoroni Interstate 75 W footprint.|**Maximum:** Mass-market board, hot-swappable in seconds.|**0.58 CHF**|
||**MCU with Native LoRa** <br>(e.g., ESP32-S3 LoRa)|10.00 – 20.00 CHF|**0.5 W**|LoRa, Wi-Fi, BLE, GPIO|**Medium:** Requires custom wiring; breaks Interstate 75 footprint.|**Medium:** Readily available on the market, but relies on custom code templates.|**1.46 CHF**|
||**Built-in MCU** <br>(All-in-one Smart Display)|Included in panel|**1.5 W** (Logic only)|RS-485, Ethernet|**Low:** Bound to proprietary closed-source manufacturer SDKs.|**Low:** Monolithic setup; cannot change the processor core.|**4.37 CHF**|

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
|LED Matrix (HUB75)|**1. [RGB P3 Matrix Panel 64x64 (2x)](https://www.waveshare.com/rgb-matrix-p3-64x64.htm)**|~72 CHF per place|**16 W** <br>(2 panels, max. 40 W)|HUB75, 5 V supply per panel|**Maximum:** Native fit with Interstate 75 W + Pico W|**High:** Standard panels, chainable|**46.60 CHF**|
|ePaper / E-Ink|**2. [E-Ink Color Display 7.3" Spectra 6](https://core-electronics.com.au/7-3inch-6-color-e-paper-display-e-ink-hat.html)**|~90–120 CHF per place|**0.07 W** <br>(max. during refresh, standby ≈ 0)|SPI (3.3 V / 5 V)|**High:** Pico W / ESP32 / Raspberry Pi, SPI demo code|**Medium:** Waveshare-specific|**0.20 CHF**|
||**3. [ePaper 10.3" (IT8951 HAT)](https://www.robotshop.com/products/waveshare-103-e-paper-e-ink-display-hat-for-raspberry-pi-18721404-black-white-16-grey-scales-usb-spi-i80)**|~158 CHF per place|**0.1 W** <br>(standby; 1.2 W during refresh)|USB / SPI / I80 via IT8951|**Medium:** Built for Raspberry Pi header, Pico W needs custom code|**Medium:** Waveshare-specific|**0.29 CHF**|
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
||**LoRa HAT** (for a single-board computer / MCU as orchestrator) (one Indoor LoRaWAN Gateway must be placed next to the server)|90–130 CHF|0.1 W – 0.5 W|SPI / UART|**Hardware Module:** Requires a compatible 40-pin header on the single-board computer.|**Maximum:** Detachable board. Can be easily replaced or swapped onto a different host computer.|0.29 – 1.46 CHF|
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

|Type|Component Name|Hardware Price (Est.)|Average Power Draw|Connectivity|Compatibility|Replaceability / Scalability|Exact 1-Year Electricity Cost|
|---|---|---|---|---|---|---|---|
|MQTT (WiFi)|Built-in WiFi(no extra hardware)|-|Included in MCU|2.4 GHz WiFi (802.11 b/g/n), MQTT over TCP/IP|**Native:** Already part of the MCU; just needs `hostapd`/AP software on the Orchestrator side.|**High:** No extra hardware to replace; scaling limited only by AP client capacity|Included in MCU|
|LoRaWAN|Built-in LoRa module|-|Included in MCU(with LoRa module)|Sub-GHz (868 MHz EU), long range (2–15 km), low bandwidth|**Native:** Already part of the MCU; just needs a LoRaWAN network server running on the gateway/server side|**High:** No extra per-node hardware to replace; one gateway can serve all 8+ nodes without added cost per node.|Included in MCU(with LoRa module)<br>|
|Cable|Сat6 Ethernet + PoE Switch|~81.00 CHF (cables) + 55.00 – 110.00 CHF (PoE switch) = **136.00 – 191.00 CHF total**|**10 – 18 W** (switch + PoE overhead)|RJ45, Cat6, PoE (802.3af/at)|**Universal + PoE:** One cable carries both power and data; Needs an RJ45 Ethernet module per node to connect via cable|**Medium/High:** Short distances (3–18m) keep installation cheap and simple; swapping a cable is trivial|34.80 – 52.20 CHF|

##### Pros and cons:

**MQTT (WiFi)**

- **Pros:**
    - Zero Extra Hardware: WiFi radio is already built into the MCU — nothing to buy or install per node.
    - Fastest Deployment: No cables, no gateway setup — just join the network and start publishing.
- **Cons:**
    - Shared Airwaves: Signal quality drops with distance, concrete walls, or interference from other 2.4 GHz devices.
    - Single Point of Congestion: All nodes compete for the same access point; too many devices can saturate it.

**LoRaWAN**

- **Pros:**
    - Massive Range: A single gateway can reach nodes kilometers away, even through walls and obstacles.
    - Lowest Power Draw: Ideal for nodes that need to run for long periods on minimal energy.
- **Cons:**
    - Thin Data Pipe: Bandwidth is too low for frequent updates or anything beyond small data packets.
    - Extra Server-Side Setup: Requires a LoRaWAN network server (e.g. ChirpStack) running and maintained on the gateway.

**Cable**

- **Pros:**
    - Infinite Data Flow: No network packet limits or wireless lag; moves heavy logging or debug files seamlessly.
    - Zero Interference Shadows: Completely unaffected by walls, distance, or wireless congestion — plus PoE delivers power and data over the same line.
- **Cons:**
    - Fixed Physical Routing: Each node needs its own cable run; relocating a node later means re-running cable.
    - Added Per-Node Hardware: Needs an RJ45 Ethernet module per node, on top of the cable and switch cost.

---