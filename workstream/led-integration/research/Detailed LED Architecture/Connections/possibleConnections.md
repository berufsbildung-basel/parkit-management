
# Connection: PARKIT → Raspberry Pi → 8 MCUs

## Overview

The goal is to select suitable communication methods between PARKIT, the Raspberry Pi, and 8 MCUs.

**System architecture:**

PARKIT (Ruby on Rails / Heroku) → 4G/LTE → Raspberry Pi → 8 MCUs → 16 LED Matrices

- PARKIT provides parking data (status, license plate, reservation time).
- Raspberry Pi retrieves updates every 60 seconds.
- Each MCU controls one parking space with 2 LED matrices.
- Each MCU receives only its assigned parking data.


## 2. Raspberry Pi → 8 MCUs

The Raspberry Pi distributes parking data individually to 8 MCUs. Each MCU controls 2 LED matrices.

### Connection Options

| Method     | Explanation                                                           | Hardware / Cables                                   | Advantages                           | Disadvantages                       | Suitability   |
| ---------- | --------------------------------------------------------------------- | --------------------------------------------------- | ------------------------------------ | ----------------------------------- | ------------- |
| **RS-485** | Serial communication over a shared cable bus using device addresses.  | USB-RS485 adapter, transceivers, twisted-pair cable | Long distances, robust, fewer cables | Extra hardware, addressing required | **Very good** |
| Ethernet   | Each MCU communicates over a wired network using its own IP address.  | Ethernet interfaces, switch, LAN cables             | Stable, individual addressing        | More hardware and cables            | Very good     |
| USB Serial | Each MCU connects directly to the Raspberry Pi through USB.           | USB interfaces, powered USB hub                     | Simple, reliable                     | Limited cable length                | Good          |
| Wi-Fi      | MCUs exchange data wirelessly over a local network.                   | Wi-Fi MCUs, access point                            | No data cables, flexible             | Interference, connection loss       | Good          |


### RS-485

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

