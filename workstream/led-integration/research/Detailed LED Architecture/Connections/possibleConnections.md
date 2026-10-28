
# Connection: Parkit → Raspberry Pi → MCUs

## Overview

This document covers:

- Connection options between PARKIT, Raspberry Pi, and 8 MCUs.
- Reusable hardware and software.
- Required protocols, cables, and adapters.
- Individual data transfer to each MCU.
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
| MQTT | PARKIT publishes data through an MQTT broker. | Low bandwidth, real-time updates. | Requires a broker and additional setup. |
| WebSockets | Raspberry Pi maintains a connection to PARKIT. | Real-time, bidirectional communication. | Connection management, more complex. |

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

Each MCU should only process data for its own parking space.

We need a reliable connection with individual addressing.

### Connection Options

| Method | How it works | Advantages | Disadvantages |
|---|---|---|---|
| RS-485 | All MCUs share a serial bus with unique addresses. | Long distances, robust, few cables. | Requires transceivers and bus setup. |
| Ethernet | Each MCU connects through a network switch. | Stable, individual IP addresses. | More cables, Ethernet hardware required. |
| USB Serial | Each MCU connects to the Raspberry Pi via USB. | Simple, reliable, easy to debug. | Short cables, USB hub needed. |
| Wi-Fi | Each MCU connects to a Wi-Fi network. | Wireless, flexible, easy to expand. | Interference, connection loss. |
| CAN Bus | MCUs share a bus with message identifiers. | Robust, good error detection. | Additional hardware and configuration. |

### Comparison Based on Project Requirements

| Method | 8 MCUs | Long Distance | Extra Hardware | Suitability |
|---|---|---|---|---|
| RS-485 | Yes | Yes | RS-485 transceivers | Very good |
| Ethernet | Yes | Yes | Switch / Ethernet interfaces | Very good |
| USB Serial | Yes | No | USB hub / adapters | Good for short distances |
| Wi-Fi | Yes | Depends on signal | Wi-Fi MCUs / access point | Good |
| CAN Bus | Yes | Yes, depending on speed | CAN controllers / transceivers | Very good |

### How to Send Different Data to Each MCU

Each MCU has a unique ID.

Each MCU controls one parking space with two LED matrices.

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

**Process:**

1. Raspberry Pi receives all parking data.
2. Raspberry Pi filters the data for each MCU.
3. Raspberry Pi sends the status to the correct MCU.
4. MCU updates both LED matrices.

**Example message:**

```json
{
  "mcu_id": 1,
  "parking_space": "P1",
  "status": "RESERVED"
}
```

With Ethernet, USB, or Wi-Fi, data can be sent directly to each MCU.

With RS-485 or CAN Bus, the MCUs share a bus and filter messages by address or identifier.

Only the correct MCU processes the message.


## 3. Reusable Hardware and Software

**Possible reusable components:**

- PARKIT Ruby on Rails application.
- Existing Raspberry Pi.
- Existing 8 MCUs.
- Existing 16 LED matrices.
- Existing power supplies and cables.
- Existing MCU firmware.

**To check:**

- Which MCU model is used?
- Which interfaces do the MCUs support?
- What is the distance between the devices?
- Are communication cables already installed?
- Can the existing firmware process addressed messages?


## 4. Required Components

### Parkit → Raspberry Pi

**Hardware:**

- Raspberry Pi
- 4G/LTE modem
- SIM card
- Power supply
- LTE antenna if required

**Software:**

- Ruby on Rails REST API
- Python application on Raspberry Pi
- HTTP client library

**Protocols:**

- HTTPS
- TCP/IP
- JSON


### Raspberry Pi → MCUs

| Method | Hardware / Adapters | Cables | Protocol |
|---|---|---|---|
| RS-485 | RS-485 transceivers, USB-RS485 adapter | Twisted-pair bus cable | Modbus RTU or custom serial |
| Ethernet | Ethernet interfaces, switch | Ethernet cables | TCP/IP |
| USB Serial | USB interfaces, powered hub if needed | USB cables | USB Serial |
| Wi-Fi | Wi-Fi MCUs, access point | None for data | TCP/IP, HTTP or MQTT |
| CAN Bus | CAN controllers and transceivers | Twisted-pair bus cable | CAN |

**Additional requirements:**

- MCU firmware for the selected protocol.
- Unique MCU addresses.
- Message validation.
- Error handling and timeouts.
- Suitable power supplies.


## 5. Recommended Options

### Parkit → Raspberry Pi

**Recommended: HTTP REST API**

- Works directly with Ruby on Rails.
- Simple implementation.
- Suitable for 60-second requests.
- No permanent connection needed.


### Raspberry Pi → MCUs

**Option 1: RS-485**

- Good for longer distances.
- Supports all 8 MCUs on one bus.
- Reliable wired communication.

**Option 2: Ethernet**

- Stable wired connection.
- Individual IP addresses.
- Good for larger installations.

**Option 3: USB Serial**

- Simple implementation.
- Good for short distances.
- Separate connection to each MCU.

**Option 4: Wi-Fi**

- No communication cables.
- Flexible installation.
- Depends on signal quality.

**Option 5: CAN Bus**

- Robust communication.
- Good error detection.
- Suitable for multiple MCUs.

**Final selection:**

RS-485 is a strong option for multiple MCUs over longer distances.

Ethernet is a good alternative if the MCUs support it.

USB is suitable when all MCUs are close to the Raspberry Pi.

Wi-Fi is useful when cables should be avoided.

CAN Bus is suitable if compatible hardware is already available.


## 6. Risks and Limitations

### Parkit → Raspberry Pi

| Risk | Solution |
|---|---|
| LTE connection loss | Automatic reconnect and retry. |
| Heroku unavailable | Handle missing data and retry. |
| Outdated data | Check timestamps. |
| Unauthorized access | HTTPS and API tokens. |
| Invalid JSON | Validate responses. |
| Power failure | Reliable power supply and automatic startup. |

### Raspberry Pi → MCUs

| Risk | Solution |
|---|---|
| Communication loss | Timeouts and retries. |
| Wrong MCU receives data | Unique addresses and validation. |
| Incorrect parking mapping | Fixed MCU-to-parking-space mapping. |
| Cable damage or interference | Suitable cables and shielding. |
| Wireless interference | Check signal strength and coverage. |
| MCU failure | Detect missing acknowledgements. |
| Outdated LED status | Use timeouts and a defined fallback display. |
| Power failure | Stable power supplies. |


## 7. Conclusion

**Parkit → Raspberry Pi:**

HTTP REST API is the recommended solution.

**Raspberry Pi → MCUs:**

The most suitable options are:

- RS-485
- Ethernet
- USB Serial
- Wi-Fi
- CAN Bus

The final choice depends on the existing MCU hardware, available interfaces, and distances between devices.
