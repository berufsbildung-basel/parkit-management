# Parking Place Panels V2 – API Documentation


## 1. Übersicht

Die Parking Place Panels unterstützen zwei unterschiedliche Parkplatztypen:

- **CAR:** Einzelne Autoparkplätze (V1, V2, V3, V4)
- **MOTORCYCLE:** Motorradparkplätze mit mehreren Stellplätzen (P45)

Die API liefert den aktuellen Parkplatzstatus und alle benötigten Informationen für die Darstellung auf den Panels.

### Unterstützte Status

| Status | Beschreibung |
|---|---|
| FREE | Parkplatz ist frei |
| RESERVED | Parkplatz ist reserviert |
| OCCUPIED | Parkplatz ist belegt |
| NO_DATA | Keine gültigen Daten verfügbar |

---

## 2. CAR – FREE

Der Parkplatz ist frei.

Das Panel zeigt den Status `FREE` und die Uhrzeit, bis wann der Parkplatz verfügbar ist.

### JSON Response

```json
{
  "panelId": "54",
  "type": "CAR",
  "status": "FREE",
  "licensePlate": null,
  "country": null,
  "availableUntil": "2026-11-03T12:00:00+01:00",
  "startTime": null,
  "endTime": null
}
```

### Panel-Anzeige

- Status: FREE
- Verfügbar bis: 12:00
- Kennzeichen: Nicht angezeigt

---

## 3. CAR – RESERVED

Der Parkplatz ist reserviert.

Das Panel zeigt den Status `RESERVED`, das Kennzeichen und die Endzeit der Reservierung.

### JSON Response

```json
{
  "panelId": "54",
  "type": "CAR",
  "status": "RESERVED",
  "licensePlate": "BS 123456",
  "country": "CH",
  "availableUntil": null,
  "startTime": "2026-11-03T12:00:00+01:00",
  "endTime": "2026-11-03T14:00:00+01:00"
}
```

### Panel-Anzeige

- Status: RESERVED
- Kennzeichen: BS 123456
- Land: CH
- Reservierung von: 12:00
- Reservierung bis: 14:00

---

## 4. CAR – OCCUPIED

Der Parkplatz ist belegt.

Das Panel zeigt den Status `OCCUPIED`, das Kennzeichen und die erwartete Endzeit der Belegung.

### JSON Response

```json
{
  "panelId": "54",
  "type": "CAR",
  "status": "OCCUPIED",
  "licensePlate": "BS 123456",
  "country": "CH",
  "availableUntil": null,
  "startTime": "2026-11-03T17:00:00+01:00",
  "endTime": "2026-11-03T19:00:00+01:00"
}
```

### Panel-Anzeige

- Status: OCCUPIED
- Kennzeichen: BS 123456
- Land: CH
- Belegt seit: 17:00
- Voraussichtlich belegt bis: 19:00



---

## 6. MOTORCYCLE – P45

Bei Motorradparkplätzen werden mehrere Stellplätze zusammengefasst.

Die API liefert die Gesamtanzahl sowie die Anzahl freier, belegter und reservierter Stellplätze.

### JSON Response

```json
{
  "panelId": "45",
  "type": "MOTORCYCLE",
  "status": "FREE",
  "totalSpaces": 6,
  "availableSpaces": 2,
  "occupiedSpaces": 4,
  "reservedSpaces": 0,
  "availableUntil": "2026-11-03T12:00:00+01:00"
}
```

### Panel-Anzeige

- Status: FREE
- Verfügbar bis: 12:00
- Freie Plätze: 2
- Gesamtplätze: 6
- Anzeige: 2/6

### Beispiel für OCCUPIED

```json
{
  "panelId": "45",
  "type": "MOTORCYCLE",
  "status": "OCCUPIED",
  "totalSpaces": 6,
  "availableSpaces": 0,
  "occupiedSpaces": 6,
  "reservedSpaces": 0,
  "availableUntil": null
}
```

### Panel-Anzeige

- Status: OCCUPIED
- Freie Plätze: 0
- Gesamtplätze: 6
- Anzeige: 6/6

Hinweis: Bei OCCUPIED zeigt das Panel die belegten Plätze
anstelle der verfügbaren Plätze an.

---

## 7. Felddefinitionen

### CAR

| Feld | Datentyp | Beschreibung |
|---|---|---|
| panelId | string | Eindeutige Panel-ID |
| type | string | CAR |
| status | string | FREE, RESERVED, OCCUPIED, NO_DATA |
| licensePlate | string/null | Fahrzeugkennzeichen |
| country | string/null | Ländercode, z. B. CH |
| availableUntil | ISO 8601/null | Verfügbar bis |
| startTime | ISO 8601/null | Beginn der Reservierung oder Belegung |
| endTime | ISO 8601/null | Ende der Reservierung oder erwarteten Belegung |

### MOTORCYCLE

| Feld | Datentyp | Beschreibung |
|---|---|---|
| panelId | string | Eindeutige Panel-ID |
| type | string | MOTORCYCLE |
| status | string | FREE, RESERVED, OCCUPIED, NO_DATA |
| totalSpaces | integer | Gesamtanzahl Stellplätze |
| availableSpaces | integer | Anzahl verfügbarer Stellplätze |
| occupiedSpaces | integer | Anzahl belegter Stellplätze |
| reservedSpaces | integer | Anzahl reservierter Stellplätze |
| availableUntil | ISO 8601/null | Verfügbar bis |

---

### Motorcycles

GET /api/panels/motorcycles/{panelId}

Liefert die Daten für Motorradparkplätze.

Unterstützte Panel-Version:

- P45

---

## 9. Validierungsregeln

### CAR

- Bei FREE ist `licensePlate` normalerweise null.
- Bei RESERVED kann `licensePlate` angegeben werden.
- Bei OCCUPIED kann `licensePlate` angegeben werden.
- Bei NO_DATA sind alle fachlichen Datenfelder null.
- Zeitangaben werden im ISO-8601-Format übertragen.
- Die Darstellung der Uhrzeit erfolgt im Frontend.

### MOTORCYCLE

- `totalSpaces` muss grösser als 0 sein.
- `availableSpaces` darf nicht negativ sein.
- `occupiedSpaces` darf nicht negativ sein.
- `reservedSpaces` darf nicht negativ sein.
- Bei gegenseitig ausschliessenden Platzkategorien gilt:

  totalSpaces = availableSpaces + occupiedSpaces + reservedSpaces

- Wenn availableSpaces > 0, ist der Status FREE.
- Wenn availableSpaces = 0 und alle Plätze belegt sind,
  ist der Status OCCUPIED.
- Bei ungültigen oder fehlenden Daten wird NO_DATA verwendet.

---

## 10. Panel-Versionen

| Version | Parkplatztyp | Beschreibung |
|---|---|---|
| V1 | CAR | Standardanzeige |
| V2 | CAR | Alternative Logo-Darstellung |
| V3 | CAR | Alternative Zeitdarstellung |
| V4 | CAR | Uhrzeit und Kennzeichen im Vordergrund |
| P45 | MOTORCYCLE | Anzeige mehrerer Motorradstellplätze |

Die Panel-Version beeinflusst ausschliesslich die Darstellung.

Die fachlichen Parkplatzdaten bleiben für V1 bis V4 identisch.

---

## 11. Empfehlung

Es werden zwei unterschiedliche API-Response-Typen verwendet:

1. CAR
2. MOTORCYCLE

Für CAR werden die Zustände FREE, RESERVED, OCCUPIED
und NO_DATA unterstützt.

Für MOTORCYCLE werden zusätzlich die Stellplatzanzahlen
übertragen.

Die Panel-Version wird unabhängig von den Parkplatzdaten
konfiguriert.

Dadurch können alle Panel-Versionen dieselbe API verwenden,
ohne dass für jede Version eine eigene JSON-Struktur benötigt wird.