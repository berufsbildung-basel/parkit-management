- Overview
- Components
	- Raspberry Pi 4
	- Router
		- Linksys Router – Konfiguration
			- Router-Informationen
			- Zugriff auf die Router-Einstellungen
			- WLAN-Konfiguration
			- Netzwerk und DHCP
	- MCU
## Overview

This document will outline the configuration steps, the usernames and passwords used, and the concept of the prototype itself.

## Components

### Raspberry Pi 4



### Router

Informations about the router and the configuration you can find here:
[workstream/led-integration/research/hardware/Router](obsidian://open?vault=parkit-management&file=workstream%2Fled-integration%2Fresearch%2Fhardware%2FRouter%2FLinksys%20Router%20%E2%80%93%20Configuration)



### MCU

#### Part 1:
Task - To start with, the task was to display a simple message on the LED panel.

We connected the LED panel to the laptop like this:


image, how the connection looks like


The code written in Micropython for the LED panel will be in the “parkit-led” repository.

We installed the MicroPico plugin on a Windows laptop; this plugin is used to connect the LED panel to the laptop, launch the program, and upload the code to the LED panel.

<img width="1500" height="220" alt="image" src="https://github.com/user-attachments/assets/6024d692-6692-4002-8396-11f61f82feb7" />

To connect to the MCU, use the MicroPico: Connect command

To upload code to the LED panel, use MicroPico: Upload file to Board
