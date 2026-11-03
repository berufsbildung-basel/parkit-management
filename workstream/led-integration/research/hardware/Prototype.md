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
<<<<<<< HEAD
# Linksys Router – Configuration

## 1. Router Information

- **Model:** Linksys WRT54GL (Wireless-G 2.4 GHz)
=======
#### Linksys Router – Konfiguration

##### 1. Router-Informationen
>>>>>>> 1356cf499ebcd57d23d2e5780f7e729a0301cabd

- **Firmware:** v4.30.11

<<<<<<< HEAD
- **Gateway:** `192.168.1.1`

- **Router IP:** `192.168.1.1`


## 2. Accessing the Router Settings
=======
##### 2. Zugriff auf die Router-Einstellungen
>>>>>>> 1356cf499ebcd57d23d2e5780f7e729a0301cabd

**URL:** [http://192.168.1.1](http://192.168.1.1/)

- **Username:** `admin`

- **Password:** ParkitPTWlan1234


**Problem:** The following errors occurred when attempting to access the settings normally via Chrome:

- `400 Bad Request`

- `ERR_SSL_VERSION_OR_CIPHER_MISMATCH`


<<<<<<< HEAD
**Solution:** Open Chrome in Incognito mode (`Cmd + Shift + N`) and enter the HTTP address.

## 3. Wi-Fi Configuration
=======
##### 3. WLAN-Konfiguration
>>>>>>> 1356cf499ebcd57d23d2e5780f7e729a0301cabd

- **SSID:** `router-parkit-pt`

<<<<<<< HEAD
- **Wi-Fi Password:** ParkitPTWlan1234
=======
##### 4. Netzwerk und DHCP
>>>>>>> 1356cf499ebcd57d23d2e5780f7e729a0301cabd

- **Router Password:** ParkitPTWlan1234

- **Security Mode:** WPA2 Personal

- **Encryption:** TKIP+AES (as shown in the screenshot)


<<<<<<< HEAD
## 4. Network and DHCP

- **Router IP:** `192.168.1.1`

- **DHCP:** Enabled

- **Network:** `192.168.1.0/24`


The router automatically assigns IP addresses to connected devices.


=======
>>>>>>> 1356cf499ebcd57d23d2e5780f7e729a0301cabd
### MCU



