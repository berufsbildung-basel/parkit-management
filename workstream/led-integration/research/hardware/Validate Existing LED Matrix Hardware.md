## Contents
- Overview
- Research
	- Hardware
	- Software options
	- 


## Overview

The purpose of this document is to identify and list the hardware available for creating a working prototype. The prototype is needed to observe and test how the system functions, determine its requirements, and explore the software options that can be used

## Research

### Hardware and cables

Hardware used for the prototype:

| Component                | Qty. | Role                                                                                        |
| ------------------------ | ---- | ------------------------------------------------------------------------------------------- |
| Intel NUC                | 1    | Orchestrator: receives Parkit data, runs the MQTT broker and routes data to the controllers |
| Interstate 75 W + Pico W | 1    | MCU: receives MQTT messages and drives the LED panel                                        |
| LED Matrix Panels        | 1    | Display: Displays parking information                                                       |
|                          | 1    | Power supply for the MCU and display                                                        |

Cables used for Hardware:

| Component                 | Qty. | Role                                                           |
| ------------------------- | ---- | -------------------------------------------------------------- |
| ASUS NUC Power Cable 120W | 1    | This is for powering the Intel NUC                             |
|                           | 1    | This is for powering the lab power supply                      |
|                           | 1    | This is for powering the MCU (and the displays simultaneously) |
| 5V Power Data Cables 4Pin | 1    | This is for powering the displays.                             |
| Micro USB                 | 1    | This is for programming the MCU.                               |

### Software

### Intel NUC 

Debian

Mosquitto  ( MQTT )

Docker Compose

Uptime Kuma

### Raspberry Pi pico W

Watchdog

Thonny or mpremote

code

file with SSID, passwords etc

Pimoroni MicroPython





```
Verify that the existing LED hardware can be connected and used  
to display a simple message.

**Tasks:**

- Identify the required power supply, cable, and connector.
- Obtain/order the missing component.
- Connect the existing hardware.
- Identify/install the required library/software.
- Display a simple test message.
- Document the setup and result.

**Current blocker:**  
Required power cable/connector is missing.

**Expected outcome:**  
The existing LED hardware is tested and its basic setup,connections, and required software are documented.
```