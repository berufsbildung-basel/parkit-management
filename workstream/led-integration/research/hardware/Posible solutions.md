
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
    - **Zero Code Modification:** Runs enterprise x86 binaries natively without cross-compilation delays .
    - **Industrial Data Redundancy:** Native NVMe SSDs completely prevent filesystem corruption during sudden power drops.
    - **Offline Heavy Autonomy:** Vast processing headroom to host local booking backups if main servers crash.
    - **Active Internal Cooling:** Factory fan assembly prevents hardware thermal throttling under heavy room temperatures.
- **Cons:**
    - **High Financial Footprint:** Highest initial hardware cost (up to 650 CHF) and annual power overhead (72.82 CHF).
    - **Sealed Cabinet Risk:** Generates 25W of continuous heat; cannot be locked inside tight, unventilated electrical boxes.
    - **No Native GPIO Pins:** Requires extra external USB-to-Serial converter boxes to talk to raw hardware components.

**Raspberry Pi 4 / 5 

- **Pros:**
    - **Cost-Efficient Queueing:** Great balance of low hardware cost (60–135 CHF) and minimal power draw (14.56 CHF/year).
    - **Direct Hardware Pins:** Exposed physical GPIO layout connects directly to industrial transceivers without USB adapters.
    - **Massive Automation Libraries:** Complete Linux OS support for standard Python/Node.js display distribution scripts.
- **Cons:**
    - **MicroSD Storage Fragility:** Standard memory cards wear down fast and corrupt easily during abrupt power outages.
    - **Hidden Accessory Cost:** Requires separate purchases of industrial cases, heatsinks, and specialized power regulators for production.

---

### Microcontroller

Table of options:

|Component Name|Hardware Price (Est.)|Average Power Draw|Connectivity|Compatibility|Replaceability / Scalability|Exact 1-Year Electricity Cost|
|---|---|---|---|---|---|---|
|**Raspberry Pi Pico W**  <br>(Microcontroller chip)|6.00 – 8.00 CHF|**0.2 W**|Wi-Fi, BLE, GPIO|**Maximum:** 100% native fit with Pimoroni Interstate 75 W footprint.|**Maximum:** Mass-market board, hot-swappable in seconds.|**0.58 CHF**|
|**MCU with Native LoRa**  <br>(e.g., ESP32-S3 LoRa)|10.00 – 20.00 CHF|**0.5 W**|LoRa, Wi-Fi, BLE, GPIO|**Medium:** Requires custom wiring; breaks Interstate 75 footprint.|**Medium:** Readily available on the market, but relies on custom code templates.|**1.46 CHF**|
|**Built-in MCU**  <br>(All-in-one Smart Display)|Included in panel|**1.5 W** (Logic only)|RS-485, Ethernet|**Low:** Bound to proprietary closed-source manufacturer SDKs.|**Low:** Monolithic setup; cannot change the processor core.|**4.37 CHF**|

Pros and cons:

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




---
### Type of Connection 1

| Indoor LoRaWAN Gateway              | 70.00 – 250.00 CHF | 4 W | RS-485 Serial Bus, Ethernet  | **Native Server Ecosystem:** Runs internal LoRaWAN stacks (ChirpStack, etc.).     | **High:** Fully integrated industrial-grade chassis with standardized protocols. | 11.65 CHF |
| ----------------------------------- | ------------------ | --- | ---------------------------- | --------------------------------------------------------------------------------- | -------------------------------------------------------------------------------- | --------- |
| Single Board Computer with LoRa HAT | 85.00 – 140.00 CHF | 6 W | USB, RS-485, Wi-Fi, Ethernet | **Full OS Control:** Linux-based; runs scripts to parse and route any server APIs | **Maximum:** Full Linux OS. Open market platform compatible with any module.     | 17.48 CHF |



---
### Type of Connection 2




мікроконтролер!!!
```
Server -(cable or something else)-> Intel Nuc -> Raspberry Pi Pico W (8) -> display 

Server -(cable or something else)-> raspbery pi-> Raspberry Pi Pico W (8) -> display



Lora solutions:

Server -(cable or something else)-> LoRa Gateway->Node ->Orchestator -> Raspberry Pi  Pico W (8) -> display

Server -(cable or something else)-> LoRa Gateway-> Orchestator(node) -> Raspberry Pi Pico W (8) -> display

Server  -> LoRa Gateway->Gateway-> (with some lora modul)Raspberry Pi Pico W (8) -> display

Server  -> LoRa Gateway->Gateway->new microcontrolers with built-in lora fuctions -> display

Server  -> LoRa Gateway->Gateway-> display with built-in microcontroler with lora fuctions  

Server  -> Swisscom Server -> Swisscom Lora -> microcontoler -> displai

Server  - (type of connection)-> Orchestrator  - (type of connection)-> microcontroller  -> display   
```