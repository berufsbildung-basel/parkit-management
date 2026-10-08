
# Posible solutions

Server -(cable or something else)-> Intel Nuc -> Raspberry Pi Pico W (8) -> display 

Server -(cable or something else)-> raspbery pi-> Raspberry Pi Pico W (8) -> display



Lora solutions:

Server -(cable or something else)-> LoRa Gateway->Node ->Orchestator -> Raspberry Pi  Pico W (8) -> display

Server -(cable or something else)-> LoRa Gateway-> Orchestator(node) -> Raspberry Pi Pico W (8) -> display

Server  -> LoRa Gateway->Gateway-> (with some lora modul)Raspberry Pi Pico W (8) -> display

Server  -> LoRa Gateway->Gateway->new microcontrolers with built-in lora fuctions -> display

Server  -> LoRa Gateway->Gateway-> display with built-in microcontroler with lora fuctions  

Server  -> Swisscom Server -> Swisscom Lora -> microcontoler -> displai




# Display-Optionen für 8 Parkplätze (Tiefgarage)


1. [RGB P3 Matrix Panel 64x64 (2x)](https://www.waveshare.com/rgb-matrix-p3-64x64.htm)
2. [ePaper 10.3" (IT8951 HAT)](https://www.robotshop.com/products/waveshare-103-e-paper-e-ink-display-hat-for-raspberry-pi-18721404-black-white-16-grey-scales-usb-spi-i80)
3. [LCD HDMI 13–15" (z. B. 15.6" Monitor)](https://www.galaxus.ch/de/search?q=15.6%20zoll%20hdmi%20monitor) (Suchlink)
4. [ePaper 12.48" Rot/Schwarz/Weiss](https://www.waveshare.com/product/displays/e-paper/12.48inch-e-paper-module-b.htm)
5. [Hybrid: ePaper 10.3" + RGB Status-LED-Strip](https://www.waveshare.com/wiki/10.3inch_e-Paper_HAT) (LED-Strip: [Suchlink](https://www.galaxus.ch/de/search?q=ws2812b%20led%20strip))
6. [LCD 10.1" HDMI + Statusleuchte](https://uk.robotshop.com/products/waveshare-101-capacitive-touch-screen-lcd-b-w-case-1280800-hdmi-ips-screen-low-power-uk)
7. [E-Ink Farbdisplay 7.3" Spectra 6](https://www.waveshare.com/product/displays/7.3inch-e-paper-hat-e.htm)
8. [LED-Matrix P5 (3–4x)](https://www.robotshop.com/products/waveshare-rgb-full-color-led-matrix-panel-5mm-pitch-6432-pixels-adjustable-brightness)

> Hinweis: Die Waveshare-P5-Panels haben 64x32 Pixel (320 × 160 mm). Für Option 8 werden mehrere Panels verkettet.

## Vergleichstabelle

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

## Kurze Empfehlung

- **Beste Gesamtlösung:** Option 5 (Hybrid ePaper + LED-Strip): sehr niedrige Betriebskosten und gute Fernsicht.
- **Bestes Preis-Leistungs-Verhältnis bei Sichtbarkeit:** Option 1 (P3 Matrix): günstig und sehr hell, aber höherer Stromverbrauch.
- **Maximale Flexibilität:** Option 3 (LCD 13–15"): teurer, aber am einfachsten zu gestalten.