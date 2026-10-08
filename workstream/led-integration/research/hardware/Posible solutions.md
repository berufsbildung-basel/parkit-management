
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


## Display Options

- [RGB P3 Matrix Panel 64x64 (2x) – Waveshare / Bastelgarage](https://www.bastelgarage.ch/rgb-p3-matrix-panel-64x64-hub75)
- [ePaper 10" – Waveshare 10.3" ePaper HAT](https://www.waveshare.com/product/displays/e-paper/10.3inch-e-paper-hat.htm)
- [LCD HDMI 10" – Waveshare 10.1" HDMI LCD](https://www.waveshare.com/10.1inch-HDMI-LCD.htm)
- [ePaper 13,3" – Waveshare 13.3" ePaper](https://www.waveshare.com/13.3inch-e-paper.htm)
- [LCD HDMI 13–15" – Beispiel 15.6" HDMI Monitor](https://www.waveshare.com/product/displays/lcd-oled/lcd-oled-1.htm)
- [LED Dot-Matrix groß – Beispielprodukt](https://www.adafruit.com/product/2278)
- [RGB P4 Matrix Panel (2–3x) – Beispielprodukt](https://www.waveshare.com/rgb-matrix-p4-64x32.htm)
- [LCD 10–13" + Statusleuchte – Waveshare 10.1" HDMI LCD](https://www.waveshare.com/10.1inch-HDMI-LCD-E.htm)

| Name | ca. Kosten pro Platz | ca. Kosten für 8 Plätze | Kosten pro Jahr* | Stromverbrauch | Platz für Informationen | Lesbarkeit aus Distanz | Eignung für unser Projekt | Pro | Contra |
| :-- | :-- | :-- | :-- | :-- | :-- | :-- | :-- | :-- | :-- |
| **RGB P3 Matrix Panel 64x64 (2x)** | ~72 CHF | ~576 CHF | ~700 CHF | Hoch | ⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ | Sehr hell, große Schrift, Farben für Status möglich, zwei Panels bieten viel Fläche | Hoher Stromverbrauch, Controller und Netzteil nötig |
| **ePaper 10"** | 158 CHF | 1'264 CHF | ~5 CHF | Sehr niedrig | ⭐⭐⭐⭐ | ⭐⭐⭐⭐ | ⭐⭐⭐⭐ | Name, Kennzeichen und Zeit gut darstellbar, extrem stromsparend | Für große Schrift etwas knapp, langsame Aktualisierung |
| **LCD HDMI 10"** | 115 CHF | 920 CHF | ~100–200 CHF | Mittel | ⭐⭐⭐⭐ | ⭐⭐⭐⭐ | ⭐⭐⭐⭐ | Hohe Auflösung, flexible Darstellung, einfach anzusteuern | 10" könnte für drei Informationen aus größerer Distanz etwas klein sein |
| **ePaper 13,3"** | ~250–400 CHF | ~2'000–3'200 CHF | ~5–20 CHF | Sehr niedrig | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ | Viel Platz für Name, Kennzeichen und Zeit, extrem niedriger Stromverbrauch | Sehr hohe Anschaffungskosten bei 8 Parkplätzen |
| **LCD HDMI 13–15"** | ~130–250 CHF | ~1'040–2'000 CHF | ~150–300 CHF | Mittel | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ | Viel Platz, große Schrift, hohe Auflösung und sehr flexible Darstellung | Höherer Stromverbrauch und teurer als LED-Matrix |
| **LED Dot-Matrix groß** | ~80–150 CHF | ~640–1'200 CHF | ~250–450 CHF | Mittel | ⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐ | Sehr gute Lesbarkeit aus Distanz und große Schrift möglich | Begrenzte Auflösung für Name + Kennzeichen + Zeit |
| **RGB P4 Matrix Panel (2–3x)** | ~70–150 CHF | ~560–1'200 CHF | ~400–600 CHF | Hoch | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐ | Große Anzeige, sehr gut sichtbar und relativ günstig | Gröbere Pixel als P3 und hoher Stromverbrauch |
| **LCD 10–13" + Statusleuchte** | ~120–200 CHF | ~960–1'600 CHF | ~100–250 CHF | Mittel | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ | Status aus Distanz sofort sichtbar, LCD zeigt Name, Kennzeichen und Zeit | Zusätzliche Hardware, Verkabelung und Steuerung nötig |

\* Die jährlichen Kosten sind grobe Schätzwerte für den Strombetrieb bei dauerhaft eingeschalteten Displays. Bei ePaper ist der Verbrauch im statischen Zustand sehr gering; die tatsächlichen Kosten hängen vom konkreten Modell und Strompreis ab.

# Display-Optionen für 8 Parkplätze (Tiefgarage)

## Übersicht & Bezugsquellen

| # | Option | Hersteller-/Produktseite | Händler / Bezugsquelle |
|---|---|---|---|
| 1 | RGB P3 Matrix Panel 64x64 (2x) | [Waveshare RGB-Matrix-P3-64x64](https://www.waveshare.com/rgb-matrix-p3-64x64.htm) | Waveshare direkt; Schweizer Händler (z. B. Bastelgarage) bitte nach "RGB Matrix P3 64x64" suchen |
| 2 | ePaper 10.3" (IT8951 HAT) | [Waveshare Wiki 10.3inch e-Paper HAT](https://www.waveshare.com/wiki/10.3inch_e-Paper_HAT) | [RobotShop](https://www.robotshop.com/products/waveshare-103-e-paper-e-ink-display-hat-for-raspberry-pi-18721404-black-white-16-grey-scales-usb-spi-i80), [Eckstein-Shop (DE)](https://eckstein-shop.de/WaveShare103inche-Papere-InkDisplayHATForRaspberryPi2C1872C39714042CBlack2FWhite2C16GreyScales2CUSB2FSPI2FI80EN) |
| 3 | LCD HDMI 13–15" (z. B. 15.6" Monitor) | Kein konkretes Produkt gefunden | [Suche bei Galaxus](https://www.galaxus.ch/de/search?q=15.6%20zoll%20hdmi%20monitor) (Suchlink) |
| 4 | ePaper 12.48" Rot/Schwarz/Weiss | [Waveshare 12.48inch e-Paper Module (B)](https://www.waveshare.com/product/displays/e-paper/12.48inch-e-paper-module-b.htm) | Waveshare direkt |
| 5 | Hybrid: ePaper 10.3" + RGB Status-LED-Strip | ePaper: [Waveshare 10.3inch e-Paper HAT](https://www.waveshare.com/wiki/10.3inch_e-Paper_HAT) | LED-Strip: kein konkretes Produkt verifiziert, z. B. [Suche bei Galaxus](https://www.galaxus.ch/de/search?q=ws2812b%20led%20strip) (Suchlink) |
| 6 | LCD 10.1" HDMI + Statusleuchte | [Waveshare Wiki 10.1inch HDMI LCD (B)](https://waveshare.com/wiki/10.1inch_HDMI_LCD_(B)) | [RobotShop UK](https://uk.robotshop.com/products/waveshare-101-capacitive-touch-screen-lcd-b-w-case-1280800-hdmi-ips-screen-low-power-uk), [Eckstein-Shop (DE)](https://eckstein-shop.de/Top__1280x800_1); Statusleuchte separat |
| 7 | E-Ink Farbdisplay 7.3" Spectra 6 | [Waveshare 7.3inch e-Paper HAT (E)](https://www.waveshare.com/product/displays/7.3inch-e-paper-hat-e.htm) | [Core Electronics (AU)](https://core-electronics.com.au/7-3inch-6-color-e-paper-display-e-ink-hat.html), [Eckstein-Shop (DE)](https://eckstein-shop.de/Neu_2__73_4) |
| 8 | LED-Matrix P5 (3–4x) | [Waveshare RGB-Matrix-P5-64x32](https://www.waveshare.com/product/rgb-matrix-p5-64x32.htm) | [RobotShop](https://www.robotshop.com/products/waveshare-rgb-full-color-led-matrix-panel-5mm-pitch-6432-pixels-adjustable-brightness) |

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