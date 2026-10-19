
1. **Parking information**
    - The system must display the parking space assigned to the driver's reservation.
    - The displayed information must match the current reservation data in Parkit.
    - The displayed information must be updated when the reservation or assigned parking space changes.
    - The parking space must be clearly identifiable by the driver.
2. **Reservation periods**
    - The system must support the reservation periods used by Parkit, including morning, afternoon, and full-day reservations.
    - The system must correctly show when a parking space becomes available again.
    - Availability information such as FREE UNTIL 12:00 should be supported where needed.
3. **Licence plates**
    - The system must support the licence plate formats required by the project.
    - Different licence plate lengths and supported characters must be handled.
    - A consistent format for displaying licence plates must be defined.

• • Privacy must be considered when licence plate information is displayed


---

## Neue Notizen

**Matrix 128x64:**

Auflösung:

128x64 Pixel

Abstand Rand:

1x1

Nutzbare Fläche:

126x62 Pixel

Hintergrund:

Schwarz

**Zeichen anzahl auf matrix 128x64:**

Bei masstab 2x2 können maximal 12 zeichen (10x10) pro zeile dargestellt werden.

Für die ganze Matrix können theoretisch 72 zeichen auf 6 Zeilen dargestellt werden.

Ohne zusätzlichen Zeichenabstand und Adobe Logo.

**Adobe Logo 128x64:**

Farbe:

Rot (#FF0000)

Schriftgrösse:

masstab 2x2

Position:

Unten rechts

Abstand Rand:

1 Pixel

---

## Parkit Integration

**Verbindung:**

- Parkit API
    
- Backend / Controller
    
- LED Matrix
    
- Jede Matrix hat eine eigene Parkplatz-ID
    

**Daten:**

- Parkplatznummer
    
- Nummernschild
    
- Reservierungsbeginn
    
- Reservierungsende
    
- Reservierungsstatus
    

**Aktualisierung:**

- Neue Reservierung
    
- Änderung der Reservierung
    
- Stornierung
    
- Änderung des Parkplatzes
    
- Beginn / Ende der Reservierung
    
- Automatische Synchronisierung mit Parkit
    

**Verbindungsfehler:**

- Anzeige: `NO DATA`
    
- Keine falschen Informationen anzeigen
    
- Erneuter Verbindungsversuch
    

---

## Reservation Handling

**Reservierungszeiten:**

Morning:

08:00–12:00

Afternoon:

12:00–18:00

Full Day:

08:00–18:00

Zeiten sind Beispiele. Tatsächliche Zeiten kommen aus Parkit.

**Anzeige:**

Reserviert:

`BS 123456`

Frei:

`FREE`

Frei bis:

`FREE UNTIL 12:00`

Ganzer Tag frei:

`FREE ALL DAY`

**Automatischer Wechsel:**

- Aktuelle Uhrzeit überprüfen
    
- Reservierungsbeginn / Ende vergleichen
    
- Nummernschild automatisch wechseln
    
- Bei keiner Reservierung `FREE` anzeigen
    

**Beispiel:**

08:00–12:00:

`BS 123456`

12:00–18:00:

`B AB 1234`

Nach 18:00:

`FREE`

---

## Licence Plates

**Unterstützte Länder:**

Schweiz:

`BS 123456`

Deutschland:

`B AB 1234`

Frankreich:

`AB-123-CD`

Italien:

`AB 123 CD`

Österreich:

`W 12345 A`

**Zeichen:**

- Buchstaben A–Z
    
- Zahlen 0–9
    
- Leerzeichen
    
- Bindestriche
    
- Weitere Sonderzeichen bei Bedarf
    

**Schriftgrösse:**

- Kurzes Nummernschild = grössere Schrift
    
- Langes Nummernschild = kleinere Schrift
    
- Automatische Anpassung
    
- Maximal verfügbare Breite beachten
    

**Format:**

- Grossbuchstaben
    
- Gleiche Schriftart
    
- Einheitlicher Zeichenabstand
    
- Nummernschild mittig anzeigen
    

---

## Privacy

**Nummernschilder:**

- Nur während der Reservierung anzeigen
    
- Nach Reservierungsende entfernen
    
- Keine Namen anzeigen
    
- Optional teilweise verdecken
    

Beispiel:

`BS ***456`


---

## Prototype

**Matrix:**

128x64 Pixel

**Hintergrund:**

Schwarz

**Schrift:**

Pixel Font

**Adobe Logo:**

Rot, unten rechts

**Anzeige Reserviert:**

```
┌────────────────────────────────────────┐
│ P12                                    │
│                                        │
│              BS 123456                 │
│                                        │
│              RESERVED                  │
│                                  adobe │
└────────────────────────────────────────┘
```

**Anzeige Frei:**

```
┌────────────────────────────────────────┐
│ P12                                    │
│                                        │
│                 FREE                   │
│              UNTIL 12:00               │
│                                        │
│                                  adobe │
└────────────────────────────────────────┘
```

**Anzeige International:**

```
┌────────────────────────────────────────┐
│ P12                                    │
│                                        │
│              B AB 1234                 │
│                                        │
│              RESERVED                  │
│                                  adobe │
└────────────────────────────────────────┘
```

**Anzeige Fehler:**

```
┌────────────────────────────────────────┐
│ P12                                    │
│                                        │
│               NO DATA                  │
│                                        │
│           CONNECTION ERROR             │
│                                  adobe │
└────────────────────────────────────────┘
```

---

## Testing

**Schrift:**

- Verschiedene Massstäbe testen
    
- Maximale Zeichenanzahl überprüfen
    
- Lesbarkeit aus Fahrzeug testen
    

**Nummernschilder:**

- Schweizer Nummernschilder
    
- Internationale Nummernschilder
    
- Lange Nummernschilder
    
- Sonderzeichen
    

**Parkit:**

- Neue Reservierung
    
- Stornierung
    
- Änderung des Parkplatzes
    
- Automatischer Wechsel
    
- Verbindungsunterbruch
    

**Anzeige:**

- Adobe Logo Position
    
- Abstand zum Rand
    
- Helligkeit
    
- Kontrast
    
- Textüberlappung
    

---

## Offene Fragen

- Mindestgrösse der Schrift?
    
- Nummernschild und Reservierungszeit gleichzeitig?
    
- Grösse des Adobe Logos?
    
- Ländercode anzeigen?
    
- Parkit API verfügbar?
    
- WLAN oder LAN?
    
- Vollständige oder teilweise verdeckte Nummernschilder?



![[Pasted image 20261019092254.png]]
