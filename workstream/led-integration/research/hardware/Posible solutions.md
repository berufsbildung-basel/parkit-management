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

1. [RGB P3 Matrix Panel 64x64 (2x)](https://www.waveshare.com/rgb-matrix-p3-64x64.htm) (Waveshare Shop)
2. [ePaper 10.3" (IT8951 HAT)](https://www.robotshop.com/products/waveshare-103-e-paper-e-ink-display-hat-for-raspberry-pi-18721404-black-white-16-grey-scales-usb-spi-i80) (RobotShop)
3. [LCD HDMI 13–15" (z. B. 15.6" Monitor)](https://www.galaxus.ch/de/search?q=15.6%20zoll%20hdmi%20monitor) (Galaxus, Suchlink)
4. [ePaper 12.48" Rot/Schwarz/Weiss](https://www.waveshare.com/product/displays/e-paper/12.48inch-e-paper-module-b.htm) (Waveshare Shop)
5. [Hybrid: ePaper 10.3" + RGB Status-LED-Strip](https://www.robotshop.com/products/waveshare-103-e-paper-e-ink-display-hat-for-raspberry-pi-18721404-black-white-16-grey-scales-usb-spi-i80) (RobotShop; LED-Strip: [Galaxus, Suchlink](https://www.galaxus.ch/de/search?q=ws2812b%20led%20strip))
6. [LCD 10.1" HDMI + Statusleuchte](https://uk.robotshop.com/products/waveshare-101-capacitive-touch-screen-lcd-b-w-case-1280800-hdmi-ips-screen-low-power-uk) (RobotShop UK)
7. [E-Ink Farbdisplay 7.3" Spectra 6](https://core-electronics.com.au/7-3inch-6-color-e-paper-display-e-ink-hat.html) (Core Electronics)
8. [LED-Matrix P5 (3–4x)](https://www.robotshop.com/products/waveshare-rgb-full-color-led-matrix-panel-5mm-pitch-6432-pixels-adjustable-brightness) (RobotShop)

> Hinweis: Die Waveshare-P5-Panels haben 64x32 Pixel (320 × 160 mm). Für Option 8 werden mehrere Panels verkettet.

##### Vergleichstabelle

| Name | ca. Kosten pro Platz | ca. Kosten für 8 Plätze | Kosten pro Jahr* | Stromverbrauch | Platz für Informationen (Textlänge & Formate) | Lesbarkeit & Sichtbarkeit aus Distanz | Gehäuseschutz & Hardware-Sicherheit (Tiefgarage) | Schnittstellen & Ansteuerung (I/O) | Netzwerksicherheit & Autorisierung | Eignung für unser Projekt | Pro | Contra |
|---|---:|---:|---:|---|---|---|---|---|---|---|---|---|
| **1. RGB P3 Matrix Panel 64x64 (2x)** | ~72 CHF | ~576 CHF | ~60–100 CHF | Hoch | ⭐⭐⭐ (Pixelbegrenzung bei langen Namen / Schilderformaten) | ⭐⭐⭐⭐⭐ (Sehr gute Sichtbarkeit beim Einfahren) | Niedrig (Offene Platine, Acryl-Schutzgehäuse nötig) | HUB75 via ESP32 / Raspberry Pi | Gut (Microcontroller mit HTTPS/MQTT) | ⭐⭐⭐⭐⭐ | Sehr hell, grosse Schrift, Signalfarben (Grün/Rot), viel Fläche | Hoher Stromverbrauch, Textlänge durch Auflösung limitiert, Zusatzgehäuse nötig |
| **2. ePaper 10.3" (Waveshare HAT)** | 158 CHF | 1'264 CHF | ~5 CHF | Sehr niedrig | ⭐⭐⭐⭐ (Gute Darstellung aller Textformate & Zeiten) | ⭐⭐⭐ (Gut nah, mässig aus Distanz) | Mittel (Stossempfindlich, Schutzglas nötig) | SPI / IT8951 Controller via RPi / MCU | Hoch (Standard-OS / verschlüsselte Protokolle) | ⭐⭐⭐⭐ | Extrem stromsparend, schneller Refresh (<1 s), Name, Kennzeichen (CH/DE/FR) und Zeit gut lesbar | Keine Signalfarben, schlechte Fernsicht im dunklen Parkhaus ohne Lampe |
| **3. LCD HDMI 13–15" (z. B. 15.6" Monitor)** | ~130–250 CHF | ~1'040–2'000 CHF | ~50–100 CHF | Mittel | ⭐⭐⭐⭐⭐ (Uneingeschränkt, Platz für Logos & Sonderzeichen) | ⭐⭐⭐⭐⭐ (Auch im Vorbeifahren gut lesbar) | Hoch (Oft robuste Metall-/VESA-Gehäuse) | HDMI / VGA / DisplayPort | Hoch (Linux/Windows Client mit VNC/HTTPS) | ⭐⭐⭐⭐⭐ | Viel Platz, grosse Schrift, hohe Auflösung, sehr flexibel | Höherer Stromverbrauch, Netzteil-Verkabelung zu jedem Platz |
| **4. ePaper 12.48" Rot/Schwarz/Weiss (Waveshare)** | ~210 CHF | ~1'680 CHF | ~5 CHF | Sehr niedrig | ⭐⭐⭐⭐⭐ (Hohe Auflösung + roter Farbakzent für Status) | ⭐⭐⭐⭐ (Gute Lesbarkeit, Rot unterstützt Fernwirkung) | Mittel (Rahmen mit Acrylglas-Schutz nötig) | SPI / USB via Raspberry Pi oder ESP32 | Hoch (WPA3/TLS) | ⭐⭐⭐⭐⭐ | Farbliche Statusanzeige (Besetzt/Frei), extrem stromsparend, viel Platz | Aktualisierung dauert ca. 37 Sek. laut Hersteller (bei Parkplätzen meist unproblematisch) |
| **5. Hybrid: ePaper 10.3" + RGB Status-LED-Strip** | ~170 CHF | ~1'360 CHF | ~10 CHF | Sehr niedrig | ⭐⭐⭐⭐ (Klare Textdarstellung + LED-Fernwirkung) | ⭐⭐⭐⭐⭐ (Farbe weithin sichtbar, Details nah lesbar) | Hoch (Kompaktes Verbundgehäuse möglich) | SPI (ePaper) + GPIO/PWM (LED-Strip) | Hoch (Saubere Trennung der Ansteuereinheiten) | ⭐⭐⭐⭐⭐ | Sehr geringer Verbrauch, beste Fernsichtbarkeit beim Einfahren | Individuelle Montage & Verkabelung der LED-Leiste |
| **6. LCD 10.1" HDMI + Statusleuchte** | ~120–200 CHF | ~960–1'600 CHF | ~35–70 CHF | Mittel | ⭐⭐⭐⭐⭐ (Details auf LCD, Fernwirkung via LED) | ⭐⭐⭐⭐⭐ (Status aus ~30 m sofort erkennbar) | Mittel-Hoch (Schutzgehäuse für LCD & LED-Bar nötig) | HDMI + GPIO / Relais für Statusleuchte | Hoch (Trennung von Ansteuerung und Status-Hardware möglich) | ⭐⭐⭐⭐⭐ | Status sofort sichtbar, LCD zeigt Name, Kennzeichen, Zeit detailliert | Zusätzliche Hardware, Verkabelung und Steuerung |
| **7. E-Ink Farbdisplay 7.3" Spectra 6 (Waveshare 7.3" ePaper HAT (E))** | ~90–120 CHF | ~720–960 CHF | ~5 CHF | Sehr niedrig | ⭐⭐⭐ (800x480 px, reicht für Name, Kennzeichen, Zeit in grosser Schrift) | ⭐⭐⭐⭐ (Mehrfarbig, aber nicht selbstleuchtend) | Mittel (Schutzgehäuse mit Acrylscheibe nötig) | SPI via ESP32 / Raspberry Pi Pico W | Hoch (ESP32/Pico mit TLS/MQTT) | ⭐⭐⭐⭐ | Günstig, mehrfarbig, extrem stromsparend, Pico-W-kompatibel | Langsame Aktualisierung (ca. 12 Sek. laut Hersteller), kleiner als 10", schlecht ohne Beleuchtung |
| **8. LED-Matrix P5 Indoor/Outdoor-Modul (3–4x)** | ~60–110 CHF | ~480–880 CHF | ~70–130 CHF | Hoch | ⭐⭐⭐⭐ (Bei 3–4 Modulen genug Fläche für 2–3 Zeilen) | ⭐⭐⭐⭐⭐ (Sehr hell, auch aus grosser Distanz lesbar) | Mittel-Hoch (Oft schon in Alu-Gehäuse, Staub-/Feuchtigkeitsschutz) | HUB75 via ESP32 / Raspberry Pi | Gut (ESP32 mit HTTPS/MQTT) | ⭐⭐⭐⭐ | Preiswert, sehr hell, robuste Bauweise, Signalfarben möglich | Grössere Pixel als P3/P4, hoher Stromverbrauch, aufwändigere Verkabelung |

\* Die Kosten pro Jahr sind grobe Schätzungen für den Dauerbetrieb (Strompreis ca. 0.25–0.30 CHF/kWh). Preise der Optionen 7 und 8 sind Richtwerte und sollten vor der Bestellung geprüft werden.

#### Pros and cons:

- **Beste Gesamtlösung:** Option 5 (Hybrid ePaper + LED-Strip): sehr niedrige Betriebskosten und gute Fernsicht.
- **Bestes Preis-Leistungs-Verhältnis bei Sichtbarkeit:** Option 1 (P3 Matrix): günstig und sehr hell, aber höherer Stromverbrauch.
- **Maximale Flexibilität:** Option 3 (LCD 13–15"): teurer, aber am einfachsten zu gestalten.

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