# Posible solutions


## Contents

- Overview
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

-  Structure: 

`Server ➔ [Type of Connection 1] ➔ Orchestrator ➔ [Type of Connection 2] ➔ Microcontroller ➔ Display`

Possible chains:

```
Server -(cable or something else)-> Intel Nuc -> Raspberry Pi Pico W (8) -> display

Server -(cable or something else)-> raspbery pi-> Raspberry Pi Pico W (8) -> display

Lora solutions:

Server -(cable or something else)-> LoRa Gateway->Node ->Orchestator -> Raspberry Pi Pico W (8) -> display

Server -(cable or something else)-> LoRa Gateway-> Orchestator(node) -> Raspberry Pi Pico W (8) -> display

Server -> LoRa Gateway->Gateway-> (with some lora modul)Raspberry Pi Pico W (8) -> display

Server -> LoRa Gateway->Gateway->new microcontrolers with built-in lora fuctions -> display

Server -> LoRa Gateway->Gateway-> display with built-in microcontroler with lora fuctions

Server -> Swisscom Server -> Swisscom Lora -> microcontoler -> displai
```


## Components


### Orchestrator 
#### Table of options:

| Component Name                                  | Hardware Price (Est.) | Average Power Draw | Connectivity               | Compatibility                                                          | Replaceability / Scalability                                                    | Exact 1-Year Electricity Cost |
| ----------------------------------------------- | --------------------- | ------------------ | -------------------------- | ---------------------------------------------------------------------- | ------------------------------------------------------------------------------- | ----------------------------- |
| **Intel NUC**  <br>(Intel Core i3 / i5 Mini PC) | 350.00 – 650.00 CHF   | **25 W**           | Ethernet, Wi-Fi, USB       | **Native:** Runs standard x86 Parkit backend binaries out-of-the-box.  | **High / Limited:** Easily hot-swapped, but physical port counts limit scaling. | **72.82 CHF**                 |
| **Raspberry Pi 4 / 5**  <br>                    | 60.00 – 135.00 CHF    | **5 W**            | Ethernet, Wi-Fi, GPIO, USB | **High:** Linux-based. Can run local script parsing and queue routing. | **High / Max:** Multi-display routing via single script orchestration.          | **14.56 CHF**                 |

#### Pros and cons:

**Intel NUC**

- **Pros:**
    - **Zero Code Modification:** Runs enterprise x86 binaries natively without cross-compilation delays.
    - **Industrial Data Redundancy:** Native NVMe SSDs completely prevent filesystem corruption during sudden power drops.
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

| Component Name | Hardware Price (Est.) | Average Power Draw | Connectivity | Compatibility | Replaceability / Scalability | Exact 1-Year Electricity Cost |
| --- | --- | --- | --- | --- | --- | --- |
| **Raspberry Pi Pico W**  <br>(Microcontroller chip) | 6.00 – 8.00 CHF | **0.2 W** | Wi-Fi, BLE, GPIO | **Maximum:** 100% native fit with Pimoroni Interstate 75 W footprint. | **Maximum:** Mass-market board, hot-swappable in seconds. | **0.58 CHF** |
| **MCU with Native LoRa**  <br>(e.g., ESP32-S3 LoRa) | 10.00 – 20.00 CHF | **0.5 W** | LoRa, Wi-Fi, BLE, GPIO | **Medium:** Requires custom wiring; breaks Interstate 75 footprint. | **Medium:** Readily available on the market, but relies on custom code templates. | **1.46 CHF** |
| **Built-in MCU**  <br>(All-in-one Smart Display) | Included in panel | **1.5 W** (Logic only) | RS-485, Ethernet | **Low:** Bound to proprietary closed-source manufacturer SDKs. | **Low:** Monolithic setup; cannot change the processor core. | **4.37 CHF** |

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
    - **Custom Circuit Overhead:** Requires fully custom PCB baseboards or complex manual wire mapping since commercial shields like the Interstate 75 cannot be used.
    - **Fragmented Code Ecosystem:** Driving HUB75 panels on ESP32 requires entirely different libraries (like ESP32-HUB75-MatrixPanel-I2S-DMA), forcing a software rewrite.

**Built-in MCU (All-in-one Smart Display)**

- **Pros:**
    - **Commercial Clean Aesthetics:** Factory-sealed industrial presentation with zero loose component wires or external development enclosures.
    - **Hardened Power Input:** Internal step-down circuits handle dirty or fluctuating garage line power without needing external brick adapters.
    - **Lower Assembly Time:** Arrives pre-built and pre-wired from the vendor, eliminating field bench assembly labor.
- **Cons:**
    - **Complete Vendor Lock-In:** Software features, security patches, and network protocols are entirely dependent on the manufacturer's updates.
    - **Monolithic Hardware Failure:** If a single component on the micro-controller fails, the entire visual display panel must be discarded and replaced.

---

### Display


#### Table of options:

| Component Name | Hardware Price (Est.) | Average Power Draw | Connectivity | Compatibility | Replaceability / Scalability | Exact 1-Year Electricity Cost |
| --- | --- | --- | --- | --- | --- | --- |
| **1. [RGB P3 Matrix Panel 64x64 (2x)](https://www.waveshare.com/rgb-matrix-p3-64x64.htm)** | ~72 CHF per place <br>(×8: ~576 CHF) | **16 W** <br>(2 panels, max. 40 W) | HUB75, separate 5 V supply per panel | **Maximum:** Native fit with Pimoroni Interstate 75 W + Pico W. | **High:** Standard HUB75 panels from many vendors, chainable. | **46.60 CHF** <br>(×8: 372.83 CHF) |
| **2. [ePaper 10.3" (IT8951 HAT)](https://www.robotshop.com/products/waveshare-103-e-paper-e-ink-display-hat-for-raspberry-pi-18721404-black-white-16-grey-scales-usb-spi-i80)** | ~158 CHF per place <br>(×8: ~1'264 CHF) | **0.1 W** <br>(Standby; 1.2 W only during refresh) | USB / SPI / I80 via IT8951 driver HAT | **Medium:** HAT is built for the Raspberry Pi 40-pin header. Pico W possible via SPI wiring, but needs custom code. | **Medium:** Waveshare-specific panel and driver board. | **0.29 CHF** <br>(×8: 2.33 CHF) |
| **3. [LCD HDMI 13–15"](https://www.galaxus.ch/de/search?q=15.6%20zoll%20hdmi%20monitor)** (e.g. 15.6" monitor, search link) | ~130–250 CHF per place <br>(×8: ~1'040–2'000 CHF) | **12 W** | HDMI + power supply | **Low–Medium:** Needs a Raspberry Pi (or similar SBC) per place. A Pico W cannot drive HDMI. | **High:** Standard monitor with VESA mount, available everywhere. | **34.95 CHF** <br>(×8: 279.62 CHF) |
| **4. [ePaper 12.48" Red/Black/White](https://www.waveshare.com/product/displays/e-paper/12.48inch-e-paper-module-b.htm)** | ~210 CHF per place <br>(×8: ~1'680 CHF) | **0.1 W** <br>(Standby, estimated) | SPI via driver board | **Medium:** Works with Raspberry Pi / ESP32. The framebuffer (~320 KB for 2 colors) exceeds the RAM of a Pico W (264 KB). | **Medium:** Waveshare-specific panel. | **0.29 CHF** <br>(×8: 2.33 CHF) |
| **5. [Hybrid: ePaper 10.3" + RGB Status LED Strip](https://www.robotshop.com/products/waveshare-103-e-paper-e-ink-display-hat-for-raspberry-pi-18721404-black-white-16-grey-scales-usb-spi-i80)** (LED strip: [search link](https://www.galaxus.ch/de/search?q=ws2812b%20led%20strip)) | ~170 CHF per place <br>(×8: ~1'360 CHF) | **2.1 W** <br>(ePaper 0.1 W + LED strip ~2 W) | USB / SPI / I80 (ePaper) + 1 GPIO data line (LED strip) | **Medium:** Same as option 2. The LED strip needs only one GPIO and runs on a Pico W. | **Medium:** ePaper is Waveshare-specific, the LED strip is standard. | **6.12 CHF** <br>(×8: 48.93 CHF) |
| **6. [LCD 10.1" HDMI + Status Light](https://uk.robotshop.com/products/waveshare-101-capacitive-touch-screen-lcd-b-w-case-1280800-hdmi-ips-screen-low-power-uk)** | ~120–200 CHF per place <br>(×8: ~960–1'600 CHF) | **5 W** <br>(LCD ~4 W + light ~1 W) | HDMI + USB, GPIO / relay for the status light | **Low–Medium:** Needs a Raspberry Pi per place (HDMI). GPIO controls the light. | **High:** Standard HDMI, any HDMI display can replace it. | **14.56 CHF** <br>(×8: 116.51 CHF) |
| **7. [E-Ink Color Display 7.3" Spectra 6](https://core-electronics.com.au/7-3inch-6-color-e-paper-display-e-ink-hat.html)** | ~90–120 CHF per place <br>(×8: ~720–960 CHF) | **0.07 W** <br>(max. during refresh, standby ≈ 0) | SPI (driver HAT, 3.3 V / 5 V) | **High:** Works with Pico W / ESP32 / Raspberry Pi, Waveshare provides SPI demo code. | **Medium:** Waveshare-specific panel. | **0.20 CHF** <br>(×8: 1.63 CHF) |
| **8. [LED Matrix P5 (3–4x)](https://www.robotshop.com/products/waveshare-rgb-full-color-led-matrix-panel-5mm-pitch-6432-pixels-adjustable-brightness)** | ~60–110 CHF per place <br>(×8: ~480–880 CHF) | **24–32 W** <br>(3–4 panels, max. 20 W each) | HUB75, separate 5 V supply per panel | **High:** Same HUB75 interface as option 1. For a chain of 3–4 panels, check the maximum resolution of the Interstate 75 W. | **High:** Standard HUB75 panels, chainable. | **69.90 – 93.21 CHF** <br>(×8: 559.24 – 745.65 CHF) |

> The P5 panels from Waveshare have 64x32 pixels (320 × 160 mm), several are chained for option 8.

#### Pros and cons:

**1. RGB P3 Matrix Panel 64x64 (2x)**

- **Pros:**
    - **Excellent Visibility:** Self-illuminating and very bright, readable when driving in and in a dark garage.
    - **Signal Colors:** Green/red status can be seen from far away.
    - **Native Pico W Fit:** Drop-in with the Interstate 75 W, low assembly effort.
- **Cons:**
    - **Limited Text Space:** Pixel limit makes long names or license plate formats tight (rated 3 of 5 stars in the earlier comparison).
    - **High Power Draw:** Highest running cost of the LED options after the P5 panels.
    - **Low Hardware Protection:** Open PCB, needs an acrylic or IP54 enclosure in the garage.

**2. ePaper 10.3" (IT8951 HAT)**

- **Pros:**
    - **Very Low Power:** Only the refresh uses energy, the image stays without power.
    - **Fast Refresh:** Full refresh under 1 s according to Waveshare, partial refresh supported.
    - **Good Text Capacity:** 1872×1404 pixels, name, license plate (CH/DE/FR) and time fit well.
- **Cons:**
    - **Poor Distance Readability:** Not self-illuminating, hard to read from a distance in a dark garage without an extra lamp.
    - **No Signal Colors:** Black/white only.
    - **Fragile:** Needs protective glass against impact.

**3. LCD HDMI 13–15"**

- **Pros:**
    - **Maximum Flexibility:** Unlimited text, logos and special characters.
    - **Excellent Readability:** Large text, readable even while driving past.
    - **Robust Housing:** Many models come with metal frames and VESA mounts.
- **Cons:**
    - **Extra SBC Per Place:** Each display needs its own Raspberry Pi, which adds cost and maintenance.
    - **Highest Running Cost of the Single Displays:** 12 W continuous.
    - **Cabling:** Power and HDMI have to be routed to every place.

**4. ePaper 12.48" Red/Black/White**

- **Pros:**
    - **Color Accent:** Red allows a simple occupied/free status.
    - **Large Area:** 1304×984 pixels, plenty of space for all information.
    - **Very Low Power:** Static image without power use.
- **Cons:**
    - **Very Slow Refresh:** About 37 s per update according to Waveshare, fine for parking spaces but not for quick changes.
    - **Needs a Stronger Controller:** The framebuffer is too big for a Pico W.
    - **Needs a Frame:** Protective acrylic or glass is needed.

**5. Hybrid: ePaper 10.3" + RGB Status LED Strip**

- **Pros:**
    - **Best Visibility Per Watt:** The LED strip shows the status from far away, the ePaper shows the details up close.
    - **Low Running Cost:** 2.1 W, about 6 CHF per year per place.
    - **Compact Housing Possible:** Both parts fit in one enclosure.
- **Cons:**
    - **Custom Assembly:** The strip needs its own mounting and wiring.
    - **Two Components Per Place:** More parts that can fail.
    - **Same Limits as Option 2:** No signal color on the ePaper itself.

**6. LCD 10.1" HDMI + Status Light**

- **Pros:**
    - **Clear Status From Far Away:** The light is visible immediately, the LCD shows the details.
    - **High Resolution:** 1280×800, flexible layout.
    - **Standard Interface:** HDMI is easy to replace.
- **Cons:**
    - **Extra SBC Per Place:** Needs a Raspberry Pi, plus GPIO or relay for the light.
    - **More Hardware:** Housing for LCD and light, more wiring.
    - **10" Can Be Small:** Three pieces of information are hard to read from a larger distance.

**7. E-Ink Color Display 7.3" Spectra 6**

- **Pros:**
    - **Low Price:** Cheapest e-paper option with color.
    - **Pico W Compatible:** SPI interface, no SBC needed.
    - **Almost No Power:** Under 0.20 CHF per year.
- **Cons:**
    - **Slow Refresh:** About 12 s according to Waveshare.
    - **Small Area:** 800×480 pixels, only large text for name, plate and time.
    - **Not Self-Illuminating:** Hard to read in a dark garage without a lamp.

**8. LED Matrix P5 (3–4x)**

- **Pros:**
    - **Very Bright:** Readable from a large distance.
    - **Low Price:** Cheapest option per place.
    - **Robust:** Often delivered with a solid frame.
- **Cons:**
    - **Coarse Pixels:** 5 mm pitch, larger than P3/P4.
    - **Highest Power Draw:** Up to 93 CHF per year per place.
    - **Complex Wiring:** Several panels and power supplies per place.

**Summary**

- **Best Overall:** Option 5 (Hybrid ePaper + LED strip): very low running cost and good visibility from far away.
- **Best Value for Visibility:** Option 1 (P3 Matrix): cheap and very bright, but higher power draw.
- **Maximum Flexibility:** Option 3 (LCD 13–15"): more expensive, but easiest to design.
---

### Type of Connection 1

#### Table of options:

| Component Name | Hardware Price (Est.) | Average Power Draw | Connectivity | Compatibility | Replaceability / Scalability | Exact 1-Year Electricity Cost |
| --- | --- | --- | --- | --- | --- | --- |
| **Indoor LoRaWAN Gateway** | 70.00 – 250.00 CHF | 4 W | RS-485 Serial Bus, Ethernet | **Native Server Ecosystem:** Runs internal LoRaWAN stacks (ChirpStack, etc.). | **High:** Fully integrated industrial-grade chassis with standardized protocols. | 11.65 CHF |
| **Single Board Computer with LoRa HAT** | 85.00 – 140.00 CHF | 6 W | USB, RS-485, Wi-Fi, Ethernet | **Full OS Control:** Linux-based; runs scripts to parse and route any server APIs | **Maximum:** Full Linux OS. Open market platform compatible with any module. | 17.48 CHF |

#### Pros and cons:

*(noch offen)*

---

### Type of Connection 2

#### Table of options:

*(noch offen)*

#### Pros and cons:

*(noch offen)*