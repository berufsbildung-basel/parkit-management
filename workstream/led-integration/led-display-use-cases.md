# P.A.R.K.I.T — LED Display Use Cases

## 1. Purpose

This document defines the different scenarios that must be considered when designing the information shown on the LED displays.

These use cases focus only on **display content and behaviour**, not on the overall LED Integration architecture.

They will be used to create, compare, and test different display designs in Storybook.

The exact layout, colours, text, and information priority will be defined during the design process.

---

## 2. Available Parking Spaces

| ID | Use Case |
|---|---|
| `DISP-UC-01` | Parking space is available for the whole day. |
| `DISP-UC-02` | Parking space is available for two or more consecutive days. |
| `DISP-UC-03` | Parking space is available in the morning (AM). |
| `DISP-UC-04` | Parking space is available in the afternoon (PM). |
| `DISP-UC-05` | Parking space is available until the next reservation. |
| `DISP-UC-06` | Parking space has no upcoming reservations. |

## 3. Reserved Parking Spaces

| ID | Use Case |
|---|---|
| `DISP-UC-07` | Parking space is reserved for the whole day. |
| `DISP-UC-08` | Parking space is reserved for two or more consecutive days. |
| `DISP-UC-09` | Parking space is reserved in the morning (AM). |
| `DISP-UC-10` | Parking space is reserved in the afternoon (PM). |
| `DISP-UC-11` | Two consecutive reservations (AM → PM). |
| `DISP-UC-12` | Multiple consecutive reservations on different days. |
| `DISP-UC-13` | Current reservation is ending soon. |
| `DISP-UC-14` | Display the next reservation (`NEXT`) with date and time. |

## 4. Guest and Special Reservations

| ID | Use Case |
|---|---|
| `DISP-UC-15` | Guest reservation with a licence plate number. |
| `DISP-UC-16` | Guest reservation without a licence plate number. |
| `DISP-UC-17` | Admin reserves a parking space for another person. |
| `DISP-UC-18` | Reservation with a long foreign licence plate number. |

## 5. Motorcycle Parking Spaces

| ID | Use Case |
|---|---|
| `DISP-UC-19` | Motorcycle parking space is available. |
| `DISP-UC-20` | Motorcycle parking space is reserved for the whole day. |
| `DISP-UC-21` | Motorcycle parking space is reserved for AM or PM. |
| `DISP-UC-22` | Motorcycle parking space is reserved for multiple days. |
| `DISP-UC-23` | Motorcycle parking space is available for multiple days. |
| `DISP-UC-24` | Two consecutive reservations for a motorcycle parking space. |
| `DISP-UC-25` | Guest reservation for a motorcycle parking space. |

## 6. Reservation Changes

| ID | Use Case |
|---|---|
| `DISP-UC-26` | Reservation is cancelled. |
| `DISP-UC-27` | Reservation date or time is changed. |
| `DISP-UC-28` | Licence plate number is changed. |
| `DISP-UC-29` | Assigned parking space is changed. |
| `DISP-UC-30` | Reservation starts. |
| `DISP-UC-31` | Reservation ends. |

## 7. Unavailability and Errors

| ID | Use Case |
|---|---|
| `DISP-UC-32` | Parking space is temporarily unavailable. |
| `DISP-UC-33` | Connection to Parkit is lost. |
| `DISP-UC-34` | Reservation data is outdated. |
| `DISP-UC-35` | Reservation data is incomplete or invalid. |

## 8. Special Display Designs

| ID | Use Case |
|---|---|
| `DISP-UC-36` | Holidays. |

---

# Notes
