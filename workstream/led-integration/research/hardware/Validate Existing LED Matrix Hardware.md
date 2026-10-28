## Contents

- Overview
- Research
	- Hardware
	- Software 
		- Raspberry Pi 4
			- Operating system
			- Data transmission
			- Remote control
		- Raspberry Pi Pico W
			- Important to keep in consideration during code development
			- Additional Files


## Overview

The purpose of this document is to identify and list the hardware available for creating a working prototype. The prototype is needed to observe and test how the system functions, determine its requirements, and explore the software options that can be used

## Research

### Hardware and cables

Hardware used for the prototype:

| Component                | Qty. | Role                                                                                        |
| ------------------------ | ---- | ------------------------------------------------------------------------------------------- |
| Raspberry Pi 4           | 1    | Orchestrator: receives Parkit data, runs the MQTT broker and routes data to the controllers |
| Interstate 75 W + Pico W | 1    | MCU: receives MQTT messages and drives the LED panel                                        |
| LED Matrix Panels        | 1    | Display: Displays parking information                                                       |
| Voltcraft ESP-3010       | 1    | Laboratory power supply unit: Power supply for the MCU and display                          |
|                          | 1    | Router                                                                                      |

Cables used for Hardware:

| Component                 | Qty. | Role                                                           |
| ------------------------- | ---- | -------------------------------------------------------------- |
| USB-C                     | 1    | This is for powering the Raspberry Pi 4                        |
|                           | 1    | This is for powering the lab power supply                      |
|                           | 1    | This is for powering the MCU (and the displays simultaneously) |
| 5V Power Data Cables 4Pin | 1    | This is for powering the displays.                             |
| Micro USB                 | 1    | This is for programming the MCU.                               |

### Software

The prototype needs to display a specific image, which requires installing, configuring, and writing specialized software

#### Raspberry Pi 4

1. **Operating system**

The Raspberry Pi 4 officially supports the following operating systems:

| Variant              | What's included                                                                            | Download size | Storage required |
| -------------------- | ------------------------------------------------------------------------------------------ | ------------- | ---------------- |
| Raspberry Pi OS      | Debian Trixie + graphical Desktop                                                          | 1 301 MB      | 6 432 MB         |
| Raspberry Pi OS Full | Debian Trixie + graphical Desktop + recommended applications (office suite, browser, etc.) | 1 969 MB      | 9 504 MB         |
| Raspberry Pi OS Lite | No graphical desktop environment at all                                                    | 525 MB        | 2 936 MB         |

For our purposes, **Raspberry Pi OS Lite** is the best fit


2. **Data transmission** AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA

**Mosquitto  ( MQTT )**
This is a system that will make it possible to send data to a specific microcontroller


3. **Remote control**

**Docker Compose**
This is a container that allows for the remote, automated restarting of specific services—running under an orchestrator—in the event of an error. It also accelerates and simplifies the process of migrating the system to another device, should the need arise


**Uptime Kuma**
This is an availability monitoring program

#### Raspberry Pi Pico W (1 version)

1. **Important to keep in consideration during code development**

**Watchdog**
A library that periodically checks whether the program is running and, if not, restarts the microcontroller

**Pimoroni MicroPython**
A library that enables control of an LED panel

2. **Additional Files**

**secrets**
There must be a configuration file (containing passwords, the MQTT broker IP address, etc.).






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