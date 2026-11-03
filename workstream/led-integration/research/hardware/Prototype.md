- Overview
- Components
	- Raspberry Pi 4
	- Router
	- MCU
## Overview

This document will outline the configuration steps, the usernames and passwords used, and the concept of the prototype itself.

## Components

### Raspberry Pi 4


### Router
# Linksys Router – Configuration

## 1. Router Information

- **Model:** Linksys WRT54GL (Wireless-G 2.4 GHz)

- **Firmware:** v4.30.11

- **Gateway:** `192.168.1.1`

- **Router IP:** `192.168.1.1`


## 2. Accessing the Router Settings

**URL:** [http://192.168.1.1](http://192.168.1.1/)

- **Username:** `admin`

- **Password:** ParkitPTWlan1234


**Problem:** The following errors occurred when attempting to access the settings normally via Chrome:

- `400 Bad Request`

- `ERR_SSL_VERSION_OR_CIPHER_MISMATCH`


**Solution:** Open Chrome in Incognito mode (`Cmd + Shift + N`) and enter the HTTP address.

## 3. Wi-Fi Configuration

- **SSID:** `router-parkit-pt`

- **Wi-Fi Password:** ParkitPTWlan1234

- **Router Password:** ParkitPTWlan1234

- **Security Mode:** WPA2 Personal

- **Encryption:** TKIP+AES (as shown in the screenshot)


## 4. Network and DHCP

- **Router IP:** `192.168.1.1`

- **DHCP:** Enabled

- **Network:** `192.168.1.0/24`


The router automatically assigns IP addresses to connected devices.


### MCU

