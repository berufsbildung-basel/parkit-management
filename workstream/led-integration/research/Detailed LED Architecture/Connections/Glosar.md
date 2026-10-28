### General Terms

| Term | Explanation |
|---|---|
| MCU (Microcontroller Unit) | Small computer that controls the two LED matrices of one parking space. |
| Raspberry Pi | Small computer that receives parking data from PARKIT and sends it to the MCUs. |
| Heroku | Cloud platform where the PARKIT application runs. |
| Ruby on Rails | Web framework used to build the PARKIT application. |
| API (Application Programming Interface) | Interface that allows applications to exchange data. |
| JSON | Text format used to exchange structured data, such as parking status and license plates. |
| Polling | Repeatedly requesting new data, in our case every 60 seconds. |
| LTE / 4G | Mobile network used by the Raspberry Pi to access the internet. |
| LED Matrix | Display made of LEDs, controlled by an MCU. |


### Communication Protocols

| Term | Explanation |
|---|---|
| HTTP REST API | Allows the Raspberry Pi to request parking data from PARKIT. |
| HTTPS | Secure HTTP communication using encryption. |
| TCP/IP | Network protocols used to transfer data between devices. |
| MQTT | Lightweight messaging protocol that uses a broker to distribute messages. |
| WebSockets | Allows continuous, bidirectional communication between two devices. |
| RS-485 | Electrical standard for serial communication between multiple devices over long distances. |
| Modbus RTU | Serial communication protocol that supports device addressing and error checking. |
| USB Serial | Serial data communication over a USB connection. |
| UART | Hardware interface for sending and receiving serial data. |
| Ethernet | Wired network technology used to connect devices. |
| Wi-Fi | Wireless network technology used to connect devices. |
| CAN Bus | Communication system that allows multiple devices to exchange messages on a shared bus. |


### Data Transfer and Hardware

| Term | Explanation |
|---|---|
| Bus | Shared communication connection used by multiple devices. |
| MCU ID / Address | Unique number used to identify an MCU. |
| Serial Communication | Data transfer where bits are sent one after another. |
| Binary Data | Data represented using bytes instead of readable text. |
| Frame | Structured message containing data and control information. |
| Transceiver | Hardware that sends and receives electrical signals. |
| Adapter | Device that connects different communication interfaces, such as USB to RS-485. |
| Broker | Server that receives and forwards MQTT messages. |
| API Token | Secret key used to authenticate requests to PARKIT. |
| Timestamp | Date and time used to check when data was created or updated. |
| Timeout | Maximum waiting time before a communication attempt is considered unsuccessful. |
| ACK (Acknowledgement) | Response confirming that a message was received. |
| Retry | Sending a request or message again after a failure. |
| Error Checking | Method used to detect corrupted or invalid messages. |
| Fallback Display | Default LED display shown when valid parking data is unavailable. |
