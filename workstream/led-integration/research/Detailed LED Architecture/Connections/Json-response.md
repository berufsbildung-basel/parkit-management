# Parking Place Panels

## 1. Overview

The Parking Place Panels support two different parking types:

- **CAR:** Individual car parking spaces (V1, V2, V3, V4)
- **MOTORCYCLE:** Motorcycle parking spaces with multiple slots (P45)

The API provides the current parking status and all the information needed to display the panels.

The following status names and availability fields are a proposed API contract for team review. PARKIT knows reservations, not physical vehicle presence. Unknown availability must not be inferred as UNAVAILABLE.

### Supported Statuses

| Status | Description |
|---|---|
| BOOKABLE | The parking space is available for booking |
| RESERVED | The parking space is reserved |
| UNAVAILABLE | The parking space is unavailable |
| NO_DATA | No valid data is available |

---

## 2. CAR – BOOKABLE

The parking space is available for booking.

The panel shows the status `BOOKABLE` and the time until the current booking availability ends.

### JSON Response

```json
{
  "panelId": "54",
  "type": "CAR",
  "status": "BOOKABLE",
  "licensePlate": null,
  "country": null,
  "availableUntil": "2026-11-03T12:00:00+01:00",
  "startTime": null,
  "endTime": null
}
```

### Panel Display

- Status: BOOKABLE
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

## 4. CAR – UNAVAILABLE

The space cannot be booked for a reason other than an active reservation. This requires an explicit availability restriction from PARKIT; the API field/source must be agreed with the team. No physical vehicle presence is inferred.

```json
{"panelId":"54","type":"CAR","status":"UNAVAILABLE","licensePlate":null,"country":null,"availableUntil":null,"startTime":null,"endTime":null}
```

## 5. NO_DATA

Missing, outdated or invalid data must display NO DATA and suppress reservation details and counts (UC-33–35). Freshness thresholds and recovery rules must follow the agreed display specification and PR #8.

## 6. MOTORCYCLE – P45

For motorcycle parking spaces, multiple parking spots are grouped together.

The API provides the total number of spaces as well as the number of available, unavailable, and reserved spaces.

### JSON Response

```json
{
  "panelId": "45",
  "type": "MOTORCYCLE",
  "status": "BOOKABLE",
  "totalSpaces": 6,
  "availableSpaces": 2,
  "unavailableSpaces": 4,
  "reservedSpaces": 0,
  "availableUntil": "2026-11-03T12:00:00+01:00"
}
```

### Panel Display

- Status: BOOKABLE
- Available until: 12:00
- Free spaces: 2
- Total spaces: 6
- Display: 2/6

### Example for UNAVAILABLE

```json
{
  "panelId": "45",
  "type": "MOTORCYCLE",
  "status": "UNAVAILABLE",
  "totalSpaces": 6,
  "availableSpaces": 0,
  "unavailableSpaces": 6,
  "reservedSpaces": 0,
  "availableUntil": null
}
```

### Panel Display

- Status: UNAVAILABLE
- Free spaces: 0
- Total spaces: 6
- Display: 0/6

The count represents bookable spaces, not detected vehicle occupancy.

---

## 7. Field Definitions

### CAR

| Field | Data Type | Description |
|---|---|---|
| panelId | string | Unique panel ID |
| type | string | CAR |
| status | string | BOOKABLE, RESERVED, UNAVAILABLE, NO_DATA |
| licensePlate | string/null | Vehicle license plate |
| country | string/null | Country code, e.g. CH |
| availableUntil | ISO 8601/null | End of current booking availability |
| startTime | ISO 8601/null | Start of reservation |
| endTime | ISO 8601/null | End of reservation |

### MOTORCYCLE

| Field | Data Type | Description |
|---|---|---|
| panelId | string | Unique panel ID |
| type | string | MOTORCYCLE |
| status | string | BOOKABLE, RESERVED, UNAVAILABLE, NO_DATA |
| totalSpaces | integer | Total number of parking spaces |
| availableSpaces | integer | Number of available parking spaces |
| unavailableSpaces | integer | Number of unavailable parking spaces |
| reservedSpaces | integer | Number of reserved parking spaces |
| availableUntil | ISO 8601/null | End of current booking availability |

---

### Motorcycles

GET /api/panels/motorcycles/{panelId}

Returns the data for motorcycle parking spaces.

Supported panel version:

- P45

---

## 9. Validation Rules

### CAR

- For BOOKABLE, `licensePlate` is usually null.
- For RESERVED, `licensePlate` may be provided.
- For UNAVAILABLE, reservation fields are null.
- For NO_DATA, all business data fields are null.
- Time values are transmitted in ISO 8601 format.
- The frontend handles the display of the time.

### MOTORCYCLE

- `totalSpaces` must be greater than 0.
- `availableSpaces` must not be negative.
- `unavailableSpaces` must not be negative.
- `reservedSpaces` must not be negative.
- For mutually exclusive space categories, the following applies:

  totalSpaces = availableSpaces + unavailableSpaces + reservedSpaces

- If `availableSpaces > 0`, the status is BOOKABLE.
- If `availableSpaces = 0` and all spaces are reserved, the status is RESERVED. If no spaces are available and at least one has an explicit non-reservation restriction, the proposed aggregate status is UNAVAILABLE.
- Outdated, invalid or missing data results in `NO_DATA`.

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

For CAR, the states BOOKABLE, RESERVED, UNAVAILABLE, and NO_DATA are supported.

For MOTORCYCLE, the number of parking spaces is also transmitted.

The panel version is configured independently from the parking data.

This allows all panel versions to use the same API without requiring a separate JSON structure for each version.
