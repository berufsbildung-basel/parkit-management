
# Connection: PARKIT → Raspberry Pi → 8 MCUs

## Overview

The goal is to select suitable communication methods between PARKIT, the Raspberry Pi, and 8 MCUs.

**System architecture:**

PARKIT (Ruby on Rails / Heroku) → 4G/LTE → Raspberry Pi → 8 MCUs → 16 LED Matrices

- PARKIT provides parking data (status, license plate, reservation time).
- Raspberry Pi retrieves updates every 60 seconds.
- Each MCU controls one parking space with 2 LED matrices.
- Each MCU receives only its assigned parking data.

## 1. PARKIT → Raspberry Pi

The Raspberry Pi communicates with PARKIT over the internet using 4G/LTE.

### Connection Options

| Method | Explanation | Advantages | Disadvantages | Suitability |
|---|---|---|---|---|
| **HTTP REST API** | Raspberry Pi periodically requests data from PARKIT via HTTPS. | Simple, supported by Rails, no permanent connection | No updates between requests | **Very good** |
| MQTT | A broker forwards messages from PARKIT to subscribed devices. | Low bandwidth, real-time updates | Requires MQTT broker | Good |
| WebSockets | Maintains a permanent connection for bidirectional data exchange. | Real-time, bidirectional | More complex, permanent connection | Moderate |

### Recommended: HTTP REST API

**Why?**

- Easy integration with Ruby on Rails.
- Suitable for 60-second updates.
- Simple HTTPS communication using JSON.
- Works with the existing LTE connection.

**Required:**
- Rails REST API endpoint
- Python HTTP client on Raspberry Pi
- HTTPS and API token
- Timeouts, retries and data validation

**Example JSON:**

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

The Raspberry Pi distributes parking data individually to 8 MCUs. Each MCU controls 2 LED matrices.

### Connection Options

| Method | Explanation | Hardware / Cables | Advantages | Disadvantages | Suitability |
|---|---|---|---|---|---|
| **RS-485** | Serial communication over a shared cable bus using device addresses. | USB-RS485 adapter, transceivers, twisted-pair cable | Long distances, robust, fewer cables | Extra hardware, addressing required | **Very good** |
| Ethernet | Each MCU communicates over a wired network using its own IP address. | Ethernet interfaces, switch, LAN cables | Stable, individual addressing | More hardware and cables | Very good |
| USB Serial | Each MCU connects directly to the Raspberry Pi through USB. | USB interfaces, powered USB hub | Simple, reliable | Limited cable length | Good |
| Wi-Fi | MCUs exchange data wirelessly over a local network. | Wi-Fi MCUs, access point | No data cables, flexible | Interference, connection loss | Good |
| CAN Bus | Multiple MCUs communicate over a shared bus with message identifiers. | CAN controllers, transceivers, bus cable | Robust, built-in error detection | More complex setup | Very good |

### Recommended: RS-485

**Why?**

- Connects all 8 MCUs using one shared bus.
- Supports longer cable distances.
- Resistant to electrical interference.
- Reduces cabling requirements.

**Communication process:**

1. Raspberry Pi retrieves JSON data from PARKIT.
2. Raspberry Pi assigns data to the correct MCU.
3. Data is sent over RS-485 with an MCU address.
4. The addressed MCU updates its 2 LED matrices.
5. MCU sends an acknowledgement (ACK).

**Example message:**

```text
1|RESERVED|BS123456|2026-10-28T15:30:00Z
```

The protocol must also include message framing, error checking and collision prevention.

**Required:**
- USB-RS485 adapter for Raspberry Pi
- RS-485 transceiver for each MCU
- Twisted-pair cable with termination
- Unique MCU addresses (1–8)
- Compatible firmware
- ACK, timeouts and retries

## 3. Existing Hardware

Before selecting the final method, check:

- Raspberry Pi and LTE hardware
- MCU models and supported interfaces
- Existing cables and distances
- MCU firmware
- Power supplies and LED matrices

Reusing existing components can reduce costs and development time.

## 4. Risks

| Risk | Solution |
|---|---|
| LTE connection loss | Retries and outdated-data detection |
| MCU communication failure | ACK, timeouts and retries |
| Incorrect parking assignment | Fixed MCU-to-parking-space mapping |
| Electrical interference | Proper cabling, termination and grounding |
| MCU failure | Fallback LED display |

## 5. Conclusion

| Connection | Recommended Method | Reason |
|---|---|---|
| PARKIT → Raspberry Pi | **HTTPS REST API** | Simple and suitable for 60-second polling |
| Raspberry Pi → 8 MCUs | **RS-485** | Robust, long distances, shared bus |

**Final recommendation:**

Use **HTTPS REST API with JSON** between PARKIT and the Raspberry Pi.

Use **RS-485 with addressed serial messages** between the Raspberry Pi and the 8 MCUs, if the existing hardware supports it.

**Open questions:**

1. Which MCU models and interfaces are available?
2. What are the cable distances?
3. Which cables are already installed?
4. Can the existing firmware be reused?
