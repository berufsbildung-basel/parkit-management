
# Connection: Parkit → Raspberry Pi → MCUs

In this document, you will find:

- Possible connections between:
    - Parkit → Raspberry Pi (mobile internet via SIM card).
    - Raspberry Pi → LED controllers (e.g., Wi-Fi, USB, RS-485, or other options).

- Information about hardware and software we can reuse.

- The required:
    - Protocols
    - Cables
    - Adapters
    - Hardware
    - Software

- An explanation of how the Raspberry Pi can send different data to the MCUs.

- A comparison table of all available options.

- The main risks.


## Connection between Parkit and Raspberry Pi

The PARKIT application runs on Heroku.

The Raspberry Pi connects to the internet via a SIM card (4G/LTE).

The Raspberry Pi should send a request to the PARKIT application every 60 seconds.

The PARKIT application should respond with the current parking data in JSON format.

For example:

**Raspberry Pi:**
"Hi Parkit, can you send me all the information?"

**PARKIT:**
`{"P1": "RESERVED", "P2": "FREE"}`

For this process, we can use the following methods:

- HTTP REST API
- MQTT
- WebSockets


### Connection Methods Comparison

| Method | Process | Advantages | Disadvantages |
|---|---|---|---|
| HTTP REST API | The Raspberry Pi sends an HTTP GET request to PARKIT every 60 seconds.<br><br>PARKIT responds with the current parking data in JSON format. | - Easy to implement and debug.<br>- Widely supported.<br>- Works well with a 60-second polling interval.<br>- No permanent connection required. | - Repeated requests even when no data changes.<br>- Updates are only received every 60 seconds.<br>- Requires a reachable API endpoint. |
| MQTT | The Raspberry Pi connects to an MQTT broker and subscribes to a topic.<br><br>PARKIT publishes parking data to this topic.<br><br>Alternatively, the Raspberry Pi publishes a request every 60 seconds, and PARKIT responds on a response topic. | - Low bandwidth usage.<br>- Lightweight protocol.<br>- Supports real-time updates.<br>- Suitable for mobile internet connections. | - Requires an MQTT broker.<br>- Additional infrastructure and configuration.<br>- Connection handling and reconnection logic are required. |
| WebSockets | The Raspberry Pi establishes a persistent WebSocket connection to PARKIT.<br><br>Every 60 seconds, it sends a request, and PARKIT returns the parking data in JSON format. | - Bidirectional communication.<br>- Low latency.<br>- Supports immediate updates without repeated HTTP connections. | - A persistent connection must be maintained.<br>- More complex reconnection handling.<br>- Mobile network interruptions can disconnect the connection. |


### Recommended Method: HTTP REST API

HTTP REST API is the best option for our project.

It is simple and works well with requests every 60 seconds.

**Process:**

1. The Raspberry Pi connects to the internet via 4G/LTE.
2. The Raspberry Pi sends an HTTPS GET request to Heroku.
3. PARKIT gets the current parking data.
4. PARKIT sends the data back in JSON format.
5. The Raspberry Pi processes the data.
6. The Raspberry Pi sends the data to the MCUs.
7. The process repeats every 60 seconds.

**Example API request:**

`GET https://parkit.herokuapp.com/api/parking/status`

**Example JSON response:**

```json
{
  "P1": "RESERVED",
  "P2": "FREE",
  "P3": "OCCUPIED"
}
```

**Important points:**

- Use HTTPS for secure communication.
- Use an API token for authentication.
- Set a timeout for requests (e.g., 10 seconds).
- Retry if the internet connection fails.
- Check if the received data is still up to date.
- Define what happens if no new data is received.


## Connection between Raspberry Pi and LED Controllers
The Raspberry Pi should send data to the eigth micro controllers the micro controllers receives only the data they need not all
how can we solve this problem?
### How the Raspberry Pi Sends Different Data to the MCUs

## Reusable Hardware and Software
Do not fill this out yet

## Required Components
All the requierd components we need to connect the three points mcu raspberry pi and PARKIT

## Options Comparison Table
All Options for the first connection 
and a table for all posible options for the second connection

## Risks
This part should include all risks that exists for this two connctions