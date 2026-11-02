# Connection: PARKIT → Raspberry Pi → 8 MCUs

## Overview

The goal is to find the most suitable communication methods between PARKIT, the Raspberry Pi, and 8 MCUs.

**System architecture:**

PARKIT (Ruby on Rails / Heroku) → 4G/LTE → Raspberry Pi → 8 MCUs → 16 LED Matrices

- PARKIT provides parking data (status, license plate, reservation time).
- Raspberry Pi retrieves the data every 60 seconds.
- Each MCU controls one parking space with 2 LED matrices.
- Each MCU must receive its own parking data.

## 1. PARKIT → Raspberry Pi

The Raspberry Pi connects to PARKIT over the internet using a 4G/LTE connection.

### Connection Options

| Method | Advantages | Disadvantages | Suitability |
|---|---|---|---|
| **HTTP REST API** | Simple, supported by Rails, no permanent connection | Updates only every 60 seconds | **Very good** |
| MQTT | Low bandwidth, real-time updates | Requires MQTT broker | Good |
| WebSockets | Real-time, bidirectional | More complex, permanent connection | Moderate |

### Recommended: HTTP REST API

**Why?**
- PARKIT already uses Ruby on Rails.
- Data only needs to be updated every 60 seconds.
- Simple implementation with HTTPS and JSON.
- Works over the existing LTE connection.

**Required:**
- Rails REST API endpoint
- Python HTTP client on Raspberry Pi
- HTTPS and API token authentication
- Timeout, retries and data validation

**Data format:** JSON

Example:
```json
{
  "P1": {
    "status": "RESERVED",
    "license_plate": "BS123456",
    "reserved_until": "2026-10-28T15:30:00Z"
  }
}
```

## 2. Raspberry Pi → 8 MCUs

The Raspberry Pi must communicate individually with 8 MCUs. Each MCU receives only the information for its assigned parking space.

### Connection Options

| Method | Hardware / Cables | Advantages | Disadvantages | Suitability |
|---|---|---|---|---|
| **RS-485** | USB-RS485 adapter, transceivers, twisted-pair cable | Long distances, robust, shared bus | Additional hardware and addressing | **Very good** |
| Ethernet | Ethernet interfaces, switch, LAN cables | Stable, individual IP addresses | More cables and hardware | Very good |
| USB Serial | USB interfaces, powered USB hub | Simple, reliable, easy to implement | Short distances | Good |
| Wi-Fi | Wi-Fi MCUs, access point | Wireless, flexible | Interference, connection loss | Good |
| CAN Bus | CAN controllers, transceivers, bus cable | Robust, built-in error detection | More complex configuration | Very good |

### Recommended: RS-485

**Why?**
- Supports multiple MCUs on one shared bus.
- Suitable for longer cable distances.
- Robust against electrical interference.
- Requires fewer cables than individual connections.

**Communication:**
1. Raspberry Pi receives JSON data from PARKIT.
2. Raspberry Pi assigns the data to the correct MCU.
3. Raspberry Pi sends an addressed message over RS-485.
4. Only the addressed MCU processes the message.
5. MCU updates its 2 LED matrices.
6. MCU sends an acknowledgement (ACK).

**Example serial message:**

```text
1|RESERVED|BS123456|2026-10-28T15:30:00Z
```

A real implementation also needs message framing, error checking and collision prevention.

**Required:**
- USB-RS485 adapter for Raspberry Pi
- RS-485 transceiver for each MCU
- Twisted-pair bus cable and termination
- Unique MCU addresses (1–8)
- MCU firmware supporting the selected protocol
- Error handling (ACK, timeout, retries)

## 3. Reusable Components

Before selecting the final connection method, check:

- Existing Raspberry Pi and LTE hardware
- MCU models and available interfaces
- Existing cables and cable distances
- Existing MCU firmware
- Existing power supplies and LED matrices

Reusing existing interfaces and cables can reduce costs and development time.

## 4. Risks and Limitations

- **LTE connection loss:** Retry requests and keep track of outdated data.
- **MCU communication failure:** Use ACK, timeouts and retries.
- **Incorrect parking data:** Use fixed MCU-to-parking-space mapping.
- **Cable interference:** Use suitable cables, termination and grounding.
- **MCU failure:** Define a fallback LED display.

## 5. Conclusion

| Connection | Recommended Method | Reason |
|---|---|---|
| PARKIT → Raspberry Pi | **HTTPS REST API** | Simple, reliable, ideal for 60-second polling |
| Raspberry Pi → 8 MCUs | **RS-485** | Robust, long distances, shared bus, fewer cables |

**Final recommendation:**

Use HTTPS REST API with JSON between PARKIT and the Raspberry Pi.

Use RS-485 with addressed serial messages between the Raspberry Pi and the 8 MCUs, provided the existing MCU hardware and installation conditions support it.

**Open questions before the final decision:**
1. Which MCU models are currently used?
2. What interfaces do the MCUs support?
3. How far apart are the Raspberry Pi and MCUs?
4. Which cables are already installed?
5. Can the existing firmware be reused?
