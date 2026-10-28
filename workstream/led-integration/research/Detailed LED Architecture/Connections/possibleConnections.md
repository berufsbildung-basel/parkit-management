
# Connection: Parkit → Raspberry Pi → MCUs

## Overview

This document covers:

- Connection options between PARKIT, Raspberry Pi, and 8 MCUs.
- Reusable hardware and software.
- Required protocols, cables, adapters, and software.
- Data formats and individual communication with each MCU.
- Comparison of communication methods.
- Main risks and limitations.


## 1. Connection between Parkit and Raspberry Pi

PARKIT is a Ruby on Rails application running on Heroku.

The Raspberry Pi connects to the internet via a SIM card (4G/LTE).

Every 60 seconds, the Raspberry Pi requests parking data from PARKIT.

PARKIT responds with JSON data.

**Example response:**

```json
{
  "P1": "RESERVED",
  "P2": "FREE",
  "P3": "OCCUPIED"
}
```

### Connection Options

| Method | How it works | Advantages | Disadvantages |
|---|---|---|---|
| HTTP REST API | Raspberry Pi sends an HTTPS GET request every 60 seconds. | Simple, supported by Rails, no permanent connection. | Repeated requests, updates every 60 seconds. |
| MQTT | PARKIT sends data through an MQTT broker. | Low bandwidth, real-time updates. | Requires a broker and additional setup. |
| WebSockets | Raspberry Pi maintains a connection to PARKIT. | Real-time, bidirectional communication. | More complex connection handling. |

### Recommended Method: HTTP REST API

HTTP REST API is the best option for our requirements.

**Process:**

1. Raspberry Pi connects via LTE.
2. Raspberry Pi sends an HTTPS GET request.
3. Rails reads the current parking data.
4. Rails responds with JSON.
5. Raspberry Pi processes the data.
6. The process repeats every 60 seconds.

**Example request:**

`GET https://your-app.herokuapp.com/api/parking/status`

**Important points:**

- Use HTTPS and API token authentication.
- Set a timeout of around 10 seconds.
- Retry failed requests.
- Check timestamps to detect outdated data.


## 2. Connection between Raspberry Pi and MCUs

The Raspberry Pi communicates with 8 MCUs.

Each MCU controls one parking space with two LED matrices.

Each MCU receives only the status of its assigned parking space.

Each MCU has a unique ID for individual communication.

### Connection Options

| Method | How it works | Advantages | Disadvantages |
|---|---|---|---|
| RS-485 | All MCUs share a serial bus with unique addresses. | Long distances, robust, few cables. | Requires transceivers and bus setup. |
| Ethernet | Each MCU connects through a network switch. | Stable, individual IP addresses. | More cables, Ethernet hardware required. |
| USB Serial | Each MCU connects via USB Serial. | Simple, reliable, easy to debug. | Short cables, USB hub needed. |
| Wi-Fi | Each MCU connects to a Wi-Fi network. | Wireless, flexible, easy to expand. | Interference, connection loss. |
| CAN Bus | MCUs share a bus using message identifiers. | Robust, good error detection. | Additional hardware and configuration. |

### Comparison Based on Project Requirements

| Method | 8 MCUs | Distance | Data Format | Suitability |
|---|---|---|---|---|
| RS-485 | Yes | Long | Serial frames | Very good |
| Ethernet | Yes | Up to 100 m per copper link | JSON over TCP/HTTP | Very good |
| USB Serial | Yes | Short | Text / JSON | Good |
| Wi-Fi | Yes | Signal-dependent | JSON over TCP/HTTP | Good |
| CAN Bus | Yes | Speed-dependent | Binary CAN frames | Very good |

### How to Send Different Data to Each MCU

The Raspberry Pi receives JSON data from PARKIT.

It filters the data and creates a separate message for each MCU.

The message format depends on the connection method.

**Possible data formats:**

- JSON: Easy to read and process, suitable for USB, Wi-Fi, and Ethernet.
- Text: Simple messages for serial communication.
- Binary: Small messages, suitable for RS-485 and CAN Bus.

**Example mapping:**

| MCU | Parking Space | LED Matrices |
|---|---|---|
| MCU 1 | P1 | 2 |
| MCU 2 | P2 | 2 |
| MCU 3 | P3 | 2 |
| MCU 4 | P4 | 2 |
| MCU 5 | P5 | 2 |
| MCU 6 | P6 | 2 |
| MCU 7 | P7 | 2 |
| MCU 8 | P8 | 2 |

**Example JSON message for MCU 1:**

```json
{
  "mcu_id": 1,
  "status": "RESERVED"
}
```

**Example simple serial message:**

`1:RESERVED\n`

- `1` = MCU address
- `RESERVED` = Parking status
- `\n` = End of message

**Example compact binary message:**

`[0x01, 0x02]`

- `0x01` = MCU address 1
- `0x02` = RESERVED status (example encoding)

For RS-485, a message also needs framing and error checking.

CAN Bus uses CAN identifiers and frames instead of this simple byte format.

**Communication process:**

1. Raspberry Pi receives all parking data from PARKIT.
2. Raspberry Pi selects the status for each MCU.
3. Raspberry Pi converts the status into the selected message format.
4. Raspberry Pi sends the message to the correct MCU.
5. MCU checks its address and reads the status.
6. MCU updates both LED matrices.
7. MCU can send an acknowledgement (ACK).

With RS-485, all MCUs share the same bus, but only the addressed MCU processes the message.

With Ethernet, USB, or Wi-Fi, messages can be sent through individual connections.


## 3. Reusable Hardware and Software

**Possible reusable components:**

- PARKIT Ruby on Rails application.
- Existing Raspberry Pi.
- Existing 8 MCUs and 16 LED matrices.
- Existing cables, power supplies, and MCU firmware.

**To check:**

- MCU models and supported interfaces.
- Distance between devices.
- Available cables and firmware compatibility.


## 4. Required Components

### Parkit → Raspberry Pi

**Hardware:**

- Raspberry Pi
- 4G/LTE modem and SIM card
- Power supply and LTE antenna if required

**Software:**

- Ruby on Rails REST API
- Python application with HTTP client

**Protocols:**

- HTTPS, TCP/IP, JSON


### Raspberry Pi → MCUs

| Method | Hardware / Adapters | Cables | Protocol |
|---|---|---|---|
| RS-485 | Transceivers, USB-RS485 adapter | Twisted-pair bus cable | Modbus RTU / custom serial |
| Ethernet | Ethernet interfaces, switch | Ethernet cables | TCP/IP, HTTP |
| USB Serial | USB interfaces, powered hub if needed | USB cables | USB Serial |
| Wi-Fi | Wi-Fi MCUs, access point | None for data | TCP/IP, HTTP / MQTT |
| CAN Bus | CAN controllers and transceivers | Twisted-pair bus cable | CAN |

**Additional requirements:**

- MCU firmware for the selected protocol.
- Unique addresses and message validation.
- Error handling and stable power supplies.


## 5. Recommended Options

### Parkit → Raspberry Pi

**Recommended: HTTP REST API**

- Supported by Ruby on Rails.
- Simple 60-second polling.
- No permanent connection required.

### Raspberry Pi → MCUs

- **RS-485:** Recommended for long distances and shared wiring.
- **Ethernet:** Stable communication with individual IP addresses.
- **USB Serial:** Simple solution for short distances.
- **Wi-Fi:** Flexible wireless installation.
- **CAN Bus:** Robust communication with error detection.

**Final selection:**

RS-485 is a strong option for 8 distributed MCUs.

For RS-485, a compact addressed serial protocol is suitable.

For USB, Ethernet, or Wi-Fi, JSON messages are easier to implement.

The final choice depends on existing MCU hardware and distances.


## 6. Risks and Limitations

### Parkit → Raspberry Pi

| Risk | Solution |
|---|---|
| LTE or Heroku connection loss | Automatic reconnect and retry. |
| Outdated or invalid data | Validate JSON and timestamps. |
| Unauthorized access | HTTPS and API tokens. |
| Power failure | Reliable power supply and automatic startup. |

### Raspberry Pi → MCUs

| Risk | Solution |
|---|---|
| Communication loss | Timeouts, ACK and retries. |
| Wrong MCU or parking data | Unique addresses and fixed mapping. |
| Corrupted messages | Framing, validation and error checking. |
| Cable damage or interference | Suitable cables and shielding. |
| Wireless interference | Check signal strength and coverage. |
| MCU failure or outdated LED status | Detect missing ACKs and use a fallback display. |


## 7. Conclusion

**Parkit → Raspberry Pi:** HTTPS REST API with JSON.

**Raspberry Pi → MCUs:** RS-485, Ethernet, USB Serial, Wi-Fi, or CAN Bus.

RS-485 with a compact serial protocol is a strong option for 8 distributed MCUs.

The final decision depends on the existing MCU interfaces, cable distances, and installation conditions.
