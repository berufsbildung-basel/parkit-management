
# Explore our existing hardware

| Datum | 29.09.2026                    |
| ----- | ----------------------------- |
| Thema | P.A.R.K.I.T                   |
|       | Explore our existing hardware |

## Contents

-  Hardware
	- Summary Table & Hardware Overview
	- Component Descriptions & Use Cases
		- RGB Matrix Panel (P3 2020 64x64-32s-m6) 
		- Interstate 75 W Driver Board
		- Raspberry Pi Pico W Microcontroller 
		- Intel NUC 13 Pro (Arena Canyon) Orchestrator


## Summary Table & Hardware Overview

| Component       | Hardware                 | Model                                                   | Use Case                                                                                                   | doc                                                                                                                                                                                                  |
| --------------- | ------------------------ | ------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Display Panel   | RGB Matrix Panel         | RGB P3 Matrix Panel 64x64 HUB75<br>p3 2020 64x64-32s-m6 | Two horizontally mounted panels displaying real-time parking space status and availability.                | [Device manual, additional documentation](https://seengreat.com/wiki/74/rgb-matrix-p3-0-64x64?srsltid=AU7gw4WkmcVyNBNv6_9192mjPoMKCqP4GaO1SOdmdPXZZzYL28sVrHxf)                                      |
| Controller      | Pimoroni Interstate 75 W | Interstate 75 W (Pico W Aboard(RP2040))                 | Connecting the microcontroller to the LED panel and the power supply.                                      | [Device guide, usage examples, and further documentation](https://github.com/pimoroni/interstate75)<br>[Connection Guide](https://learn.pimoroni.com/article/getting-started-with-interstate-75)<br> |
| Microcontroller | Raspberry Pi Pico W      | Raspberry Pi Pico W (RP2040)                            | Data acquisition and image visualization on two LED panels.                                                | [Raspberry Pi PIco W guide, further documentation](https://www.raspberrypi.com/documentation/microcontrollers/pico-series.html)                                                                      |
| Orchestrator    | Intel NUC                | Intel NUC 13 Pro (NUC13ANHi7000)                        | Retrieving data from the server, distributing the information, and transmitting it to the microcontrollers | [Device manual, additional documentation](https://download.intel.com/newsroom/2023/client-computing/Intel-NUC-13-Pro-Tech-Product-Spec.pdf)                                                          |
- [ ] prototipe
- [ ]  kabel supplie


## Component Descriptions & Use Cases

### RGB Matrix Panel

#### Description

The **P3 2020 64x64-32s-m6** is a high-density, full-color indoor **RGB LED matrix panel** measuring 192×192mm. It features a fine **3mm pixel pitch** and a native resolution of **64×64 pixels**, packing 4,096 vibrant SMD 2121 LEDs into a compact footprint. Driven via a standard **HUB75 interface** with a **1/32 multiplexing scan rate**, this display requires a dedicated **5V power supply (minimum 4A)** and an addressable "E line" connection to handle its intensive row multiplexing.

#### Use Cases

This is the display that will show information about the parking space. Two such panels will be mounted horizontally.



### Interstate 75 W 

#### Description

The Interstate 75 W (Pico W Aboard) is an all-in-one controller and driver board designed specifically for **HUB75-style RGB LED matrix panels**. Developed by Pimoroni, it features a pre-assembled **Raspberry Pi Pico W**

#### Use Cases

Connecting the microcontroller to the LED panel and power supply



### Raspberry Pi PIco W

#### Description

The **Raspberry Pi Pico W** is a compact, low-cost **microcontroller board** that adds native **2.4GHz Wi-Fi and Bluetooth** connectivity to the powerful, custom-designed **RP2040 silicon chip**. It is designed for physical computing projects, IoT applications, and embedded control, offering wireless networking in the same small form factor as the original Pico.

#### Use Cases

The Raspberry Pi Pico W is a microcontroller used to control the process of displaying images on two displays. It is integrated into the Interstate 75 W kit



### Intel NUC 

#### Description

The Intel NUC 13 Pro (NUC13ANHi7), codenamed **Arena Canyon**, is a high-performance, ultra-compact mini PC designed for professional workflows, office productivity, and home entertainment. Packaged in a space-saving 4x4 chassis, it delivers desktop-grade computing power while supporting 24/7 commercial operation

#### Use Cases

This is a orchestrator; it will distribute data to the appropriate microcontrollers, and the parking reservation service will run on it.

