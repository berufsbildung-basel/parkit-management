# Parking Place Panels

## 1. Overview

The Parking Place Panels support two different parking types:

- **CAR:** Individual car parking spaces (V1, V2, V3, V4)
- **MOTORCYCLE:** Motorcycle parking spaces with multiple slots (P45)

The API provides the current parking status and all the information needed to display the panels.

### Supported Statuses

| Status | Description |
|---|---|
| FREE | The parking space is free |
| RESERVED | The parking space is reserved |
| OCCUPIED | The parking space is occupied |
| NO_DATA | No valid data is available |

---

## 2. CAR – FREE

The parking space is free.

The panel shows the status `FREE` and the time until the parking space becomes available.

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

### Panel Display

- Status: FREE
- Available until: 12:00
- License plate: Not displayed

---

## 3. CAR – RESERVED

The parking space is reserved.

The panel shows the status `RESERVED`, the license plate, and the end time of the reservation.

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

### Panel Display

- Status: RESERVED
- License plate: BS 123456
- Country: CH
- Reservation from: 12:00
- Reservation until: 14:00

---

## 4. CAR – OCCUPIED

The parking space is occupied.

The panel shows the status `OCCUPIED`, the license plate, and the expected end time of the occupation.

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

### Panel Display

- Status: OCCUPIED
- License plate: BS 123456
- Country: CH
- Occupied since: 17:00
- Expected occupied until: 19:00

---

## 6. MOTORCYCLE – P45

For motorcycle parking spaces, multiple parking spots are grouped together.

The API provides the total number of spaces as well as the number of free, occupied, and reserved spaces.

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

### Panel Display

- Status: FREE
- Available until: 12:00
- Free spaces: 2
- Total spaces: 6
- Display: 2/6

### Example for OCCUPIED

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

### Panel Display

- Status: OCCUPIED
- Free spaces: 0
- Total spaces: 6
- Display: 6/6

Note: In the OCCUPIED state, the panel shows the occupied spaces instead of the available spaces.

---

## 7. Field Definitions

### CAR

| Field | Data Type | Description |
|---|---|---|
| panelId | string | Unique panel ID |
| type | string | CAR |
| status | string | FREE, RESERVED, OCCUPIED, NO_DATA |
| licensePlate | string/null | Vehicle license plate |
| country | string/null | Country code, e.g. CH |
| availableUntil | ISO 8601/null | Time until available |
| startTime | ISO 8601/null | Start of reservation or occupancy |
| endTime | ISO 8601/null | End of reservation or expected occupancy |

### MOTORCYCLE

| Field | Data Type | Description |
|---|---|---|
| panelId | string | Unique panel ID |
| type | string | MOTORCYCLE |
| status | string | FREE, RESERVED, OCCUPIED, NO_DATA |
| totalSpaces | integer | Total number of parking spaces |
| availableSpaces | integer | Number of available parking spaces |
| occupiedSpaces | integer | Number of occupied parking spaces |
| reservedSpaces | integer | Number of reserved parking spaces |
| availableUntil | ISO 8601/null | Time until available |

---

### Motorcycles

GET /api/panels/motorcycles/{panelId}

Returns the data for motorcycle parking spaces.

Supported panel version:

- P45

---

## 9. Validation Rules

### CAR

- For FREE, `licensePlate` is usually null.
- For RESERVED, `licensePlate` may be provided.
- For OCCUPIED, `licensePlate` may be provided.
- For NO_DATA, all business data fields are null.
- Time values are transmitted in ISO 8601 format.
- The frontend handles the display of the time.

### MOTORCYCLE

- `totalSpaces` must be greater than 0.
- `availableSpaces` must not be negative.
- `occupiedSpaces` must not be negative.
- `reservedSpaces` must not be negative.
- For mutually exclusive space categories, the following applies:

  totalSpaces = availableSpaces + occupiedSpaces + reservedSpaces

- If `availableSpaces > 0`, the status is FREE.
- If `availableSpaces = 0` and all spaces are occupied, the status is OCCUPIED.
- Invalid or missing data results in `NO_DATA`.

---

## 10. Panel Versions

| Version | Parking Type | Description |
|---|---|---|
| V1 | CAR | Standard display |
| V2 | CAR | Alternative logo display |
| V3 | CAR | Alternative time display |
| V4 | CAR | Time and license plate in the foreground |
| P45 | MOTORCYCLE | Display for multiple motorcycle spaces |

The panel version affects only the display.

The actual parking data remains identical for V1 to V4.

---

## 11. Recommendation

Two different API response types are used:

1. CAR
2. MOTORCYCLE

For CAR, the states FREE, RESERVED, OCCUPIED, and NO_DATA are supported.

For MOTORCYCLE, the number of parking spaces is also transmitted.

The panel version is configured independently from the parking data.

This allows all panel versions to use the same API without requiring a separate JSON structure for each version.