# Posible solutions

## Contents

- Overview
- Possible structure
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

## Possible structure

## Possible structure

Legend: `(×8)` = one unit per parking space.

### Solution 1: Cable + Raspberry Pi

```
Server ➔ Physical cable (Ethernet) ➔ Raspberry Pi 4/5 ➔ Wi-Fi (MQTT) ➔ Raspberry Pi Pico W (×8) ➔ Display (×8)
```

- Simplest and cheapest setup, native fit with HUB75 panels (Pico W + Interstate 75 W).
- Needs a Wi-Fi access point in the garage and the cable laying.

### Solution 2: Cable + Intel NUC

```
Server ➔ Physical cable (Ethernet) ➔ Intel NUC ➔ Wi-Fi (MQTT) ➔ Raspberry Pi Pico W (×8) ➔ Display (×8)
```

- Same as Solution 1, but the Parkit backend binaries run natively and the NVMe SSD is more robust.
- Higher hardware cost (350–650 CHF) and higher power draw than the Raspberry Pi.

### Solution 3: LoRa gateway + orchestrator with LoRa HAT

```
Server ➔ Indoor LoRaWAN Gateway ➔ LoRa ➔ Raspberry Pi + LoRa HAT (orchestrator) ➔ Wi-Fi (MQTT) ➔ Raspberry Pi Pico W (×8) ➔ Display (×8)
```

- No cable between server room and garage, but the gateway must be placed next to the server.
- Keeps the Pico W and the HUB75 displays, LoRa is only used up to the orchestrator.

### Solution 4: LoRa gateway + microcontroller with native LoRa

```
Server ➔ Indoor LoRaWAN Gateway ➔ LoRa ➔ MCU with Native LoRa, e.g. ESP32-S3 LoRa (×8) ➔ ePaper Display (×8)
```

- No orchestrator and no Wi-Fi needed.
- Best suited for ePaper: LED panels are hard to connect to LoRa boards (see Microcontroller cons).

### Solution 5: Swisscom LoRaWAN

```
Server ➔ Internet (HTTPS) ➔ Swisscom LPN LoRaWAN ➔ LoRa ➔ MCU with Native LoRa, e.g. ESP32-S3 LoRa (×8) ➔ ePaper Display (×8)
```

- No own gateway to buy or maintain, only the LPN subscription (~5.40 – 42.00 CHF/year).
- Signal coverage in the underground garage must be tested first.

### Overview

| # | Connection 1 | Orchestrator | Connection 2 | Microcontroller | Display |
| --- | --- | --- | --- | --- | --- |
| 1 | Physical cable | Raspberry Pi 4/5 | Wi-Fi (MQTT) | Raspberry Pi Pico W | Any (e.g. HUB75 panel) |
| 2 | Physical cable | Intel NUC | Wi-Fi (MQTT) | Raspberry Pi Pico W | Any (e.g. HUB75 panel) |
| 3 | LoRaWAN Gateway | Raspberry Pi + LoRa HAT | Wi-Fi (MQTT) | Raspberry Pi Pico W | Any (e.g. HUB75 panel) |
| 4 | LoRaWAN Gateway | – | LoRa | MCU with Native LoRa | ePaper |
| 5 | Swisscom LPN | – | LoRa | MCU with Native LoRa | ePaper |

```
Server -(cable or something else)-> Intel Nuc -> Raspberry Pi Pico W (8) -> display

Server -(cable or something else)-> raspbery pi-> Raspberry Pi Pico W (8) -> display





Lora solutions:

Server -(cable or something else)-> LoRa Gateway->Node ->Orchestator -> Raspberry Pi  Pico W (8) -> display

Server -(cable or something else)-> LoRa Gateway-> Orchestator(node) -> Raspberry Pi Pico W (8) -> display

Server  -> LoRa Gateway->Gateway-> (with some lora modul)Raspberry Pi Pico W (8) -> display

Server  -> LoRa Gateway->Gateway->new microcontrolers with built-in lora fuctions -> display

Server  -> LoRa Gateway->Gateway-> display with built-in microcontroler with lora fuctions

Server  -> Swisscom Server -> Swisscom Lora -> microcontoler -> displai

Server  - (type of connection)-> Orchestrator  - (type of connection)-> microcontroller  -> display
```

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


### Display


#### Table of options:

| Component Name | Hardware Price (Est.) | Average Power Draw | Connectivity | Compatibility | Replaceability / Scalability | Exact 1-Year Electricity Cost |
| --- | --- | --- | --- | --- | --- | --- |
| **1. [RGB P3 Matrix Panel 64x64 (2x)](https://www.waveshare.com/rgb-matrix-p3-64x64.htm)** | ~72 CHF per place <br> | **16 W** <br>(2 panels, max. 40 W) | HUB75, separate 5 V supply per panel | **Maximum:** Native fit with Pimoroni Interstate 75 W + Pico W. | **High:** Standard HUB75 panels from many vendors, chainable. | **46.60 CHF** <br> |
| **2. [ePaper 10.3" (IT8951 HAT)](https://www.robotshop.com/products/waveshare-103-e-paper-e-ink-display-hat-for-raspberry-pi-18721404-black-white-16-grey-scales-usb-spi-i80)** | ~158 CHF per place <br> | **0.1 W** <br>(Standby; 1.2 W only during refresh) | USB / SPI / I80 via IT8951 driver HAT | **Medium:** HAT is built for the Raspberry Pi 40-pin header. Pico W possible via SPI wiring, but needs custom code. | **Medium:** Waveshare-specific panel and driver board. | **0.29 CHF** <br> |
| **3. [LCD HDMI 13–15"](https://www.galaxus.ch/de/search?q=15.6%20zoll%20hdmi%20monitor)** (e.g. 15.6" monitor, search link) | ~130–250 CHF per place <br> | **12 W** | HDMI + power supply | **Low–Medium:** Needs a Raspberry Pi (or similar SBC) per place. A Pico W cannot drive HDMI. | **High:** Standard monitor with VESA mount, available everywhere. | **34.95 CHF** <br>|
| **4. [ePaper 12.48" Red/Black/White](https://www.waveshare.com/product/displays/e-paper/12.48inch-e-paper-module-b.htm)** | ~210 CHF per place <br> | **0.1 W** <br>(Standby, estimated) | SPI via driver board | **Medium:** Works with Raspberry Pi / ESP32. The framebuffer (~320 KB for 2 colors) exceeds the RAM of a Pico W (264 KB). | **Medium:** Waveshare-specific panel. | **0.29 CHF** <br> |
| **5. [Hybrid: ePaper 10.3" + RGB Status LED Strip](https://www.robotshop.com/products/waveshare-103-e-paper-e-ink-display-hat-for-raspberry-pi-18721404-black-white-16-grey-scales-usb-spi-i80)** (LED strip: [search link](https://www.galaxus.ch/de/search?q=ws2812b%20led%20strip)) | ~170 CHF per place <br> | **2.1 W** <br>(ePaper 0.1 W + LED strip ~2 W) | USB / SPI / I80 (ePaper) + 1 GPIO data line (LED strip) | **Medium:** Same as option 2. The LED strip needs only one GPIO and runs on a Pico W. | **Medium:** ePaper is Waveshare-specific, the LED strip is standard. | **6.12 CHF** <br> |
| **6. [LCD 10.1" HDMI + Status Light](https://uk.robotshop.com/products/waveshare-101-capacitive-touch-screen-lcd-b-w-case-1280800-hdmi-ips-screen-low-power-uk)** | ~120–200 CHF per place <br> | **5 W** <br>(LCD ~4 W + light ~1 W) | HDMI + USB, GPIO / relay for the status light | **Low–Medium:** Needs a Raspberry Pi per place (HDMI). GPIO controls the light. | **High:** Standard HDMI, any HDMI display can replace it. | **14.56 CHF** <br> |
| **7. [E-Ink Color Display 7.3" Spectra 6](https://core-electronics.com.au/7-3inch-6-color-e-paper-display-e-ink-hat.html)** | ~90–120 CHF per place <br> | **0.07 W** <br>(max. during refresh, standby ≈ 0) | SPI (driver HAT, 3.3 V / 5 V) | **High:** Works with Pico W / ESP32 / Raspberry Pi, Waveshare provides SPI demo code. | **Medium:** Waveshare-specific panel. | **0.20 CHF** <br> |
| **8. [LED Matrix P5 (3–4x)](https://www.robotshop.com/products/waveshare-rgb-full-color-led-matrix-panel-5mm-pitch-6432-pixels-adjustable-brightness)** | ~60–110 CHF per place <br> | **24–32 W** <br>(3–4 panels, max. 20 W each) | HUB75, separate 5 V supply per panel | **High:** Same HUB75 interface as option 1. For a chain of 3–4 panels, check the maximum resolution of the Interstate 75 W. | **High:** Standard HUB75 panels, chainable. | **69.90 – 93.21 CHF** <br> |





| Type                       | Component Name                                                                                                                                                                                                                                                                                    | Hardware Price (Est.)        | Average Power Draw                                      | Connectivity                                              | Compatibility                                                                                                         | Replaceability / Scalability                                              | Exact 1-Year Electricity Cost |
| -------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ---------------------------- | ------------------------------------------------------- | --------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------- | ----------------------------- |
| LED Matrix (HUB75)         | **1. [RGB P3 Matrix Panel 64x64 (2x)](https://www.waveshare.com/rgb-matrix-p3-64x64.htm)**                                                                                                                                                                                                        | ~72 CHF per place            | **16 W** <br>(2 panels, max. 40 W)                      | HUB75, separate 5 V supply per panel                      | **Maximum:** Native fit with Pimoroni Interstate 75 W + Pico W.                                                       | **High:** Standard HUB75 panels from many vendors, chainable.             | **46.60 CHF**                 |
|                            | **8. [LED Matrix P5 (3–4x)](https://www.robotshop.com/products/waveshare-rgb-full-color-led-matrix-panel-5mm-pitch-6432-pixels-adjustable-brightness)**                                                                                                                                           | ~60–110 CHF per place        | **24–32 W** <br>(3–4 panels, max. 20 W each)            | HUB75, separate 5 V supply per panel                      | **High:** Same HUB75 interface as option 1. For a chain of 3–4 panels, check the maximum resolution of the Interstate 75 W. | **High:** Standard HUB75 panels, chainable.                               | **69.90 – 93.21 CHF**         |
| ePaper / E-Ink             | **2. [ePaper 10.3" (IT8951 HAT)](https://www.robotshop.com/products/waveshare-103-e-paper-e-ink-display-hat-for-raspberry-pi-18721404-black-white-16-grey-scales-usb-spi-i80)**                                                                                                                    | ~158 CHF per place           | **0.1 W** <br>(Standby; 1.2 W only during refresh)      | USB / SPI / I80 via IT8951 driver HAT                     | **Medium:** HAT is built for the Raspberry Pi 40-pin header. Pico W possible via SPI wiring, but needs custom code.   | **Medium:** Waveshare-specific panel and driver board.                    | **0.29 CHF**                  |
|                            | **4. [ePaper 12.48" Red/Black/White](https://www.waveshare.com/product/displays/e-paper/12.48inch-e-paper-module-b.htm)**                                                                                                                                                                         | ~210 CHF per place           | **0.1 W** <br>(Standby, estimated)                      | SPI via driver board                                      | **Medium:** Works with Raspberry Pi / ESP32. The framebuffer (~320 KB for 2 colors) exceeds the RAM of a Pico W (264 KB). | **Medium:** Waveshare-specific panel.                                     | **0.29 CHF**                  |
|                            | **7. [E-Ink Color Display 7.3" Spectra 6](https://core-electronics.com.au/7-3inch-6-color-e-paper-display-e-ink-hat.html)**                                                                                                                                                                       | ~90–120 CHF per place        | **0.07 W** <br>(max. during refresh, standby ≈ 0)       | SPI (driver HAT, 3.3 V / 5 V)                             | **High:** Works with Pico W / ESP32 / Raspberry Pi, Waveshare provides SPI demo code.                                 | **Medium:** Waveshare-specific panel.                                     | **0.20 CHF**                  |
| Hybrid (ePaper + LED)      | **5. [Hybrid: ePaper 10.3" + RGB Status LED Strip](https://www.robotshop.com/products/waveshare-103-e-paper-e-ink-display-hat-for-raspberry-pi-18721404-black-white-16-grey-scales-usb-spi-i80)** (LED strip: [search link](https://www.galaxus.ch/de/search?q=ws2812b%20led%20strip))             | ~170 CHF per place           | **2.1 W** <br>(ePaper 0.1 W + LED strip ~2 W)           | USB / SPI / I80 (ePaper) + 1 GPIO data line (LED strip)   | **Medium:** Same as option 2. The LED strip needs only one GPIO and runs on a Pico W.                                 | **Medium:** ePaper is Waveshare-specific, the LED strip is standard.      | **6.12 CHF**                  |
| LCD (HDMI)                 | **3. [LCD HDMI 13–15"](https://www.galaxus.ch/de/search?q=15.6%20zoll%20hdmi%20monitor)** (e.g. 15.6" monitor, search link)                                                                                                                                                                       | ~130–250 CHF per place       | **12 W**                                                | HDMI + power supply                                       | **Low–Medium:** Needs a Raspberry Pi (or similar SBC) per place. A Pico W cannot drive HDMI.                          | **High:** Standard monitor with VESA mount, available everywhere.         | **34.95 CHF**                 |
|                            | **6. [LCD 10.1" HDMI + Status Light](https://uk.robotshop.com/products/waveshare-101-capacitive-touch-screen-lcd-b-w-case-1280800-hdmi-ips-screen-low-power-uk)**                                                                                                                                 | ~120–200 CHF per place       | **5 W** <br>(LCD ~4 W + light ~1 W)                     | HDMI + USB, GPIO / relay for the status light             | **Low–Medium:** Needs a Raspberry Pi per place (HDMI). GPIO controls the light.                                       | **High:** Standard HDMI, any HDMI display can replace it.                 | **14.56 CHF**                 |

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
