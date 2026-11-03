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
# Linksys Router – Konfiguration

## 1. Router-Informationen

- **Modell:** Linksys WRT54GL (Wireless-G 2.4 GHz)
    
- **Firmware:** v4.30.11
    
- **Gateway:** `192.168.1.1`
    
- **Router-IP:** `192.168.1.1`
    

## 2. Zugriff auf die Router-Einstellungen

**URL:** [http://192.168.1.1](http://192.168.1.1/)

- **Username:** `admin`
    
- **Passwort:** Im Passwortmanager hinterlegt
    

**Problem:** Beim normalen Zugriff über Chrome traten folgende Fehler auf:

- `400 Bad Request`
    
- `ERR_SSL_VERSION_OR_CIPHER_MISMATCH`
    

**Lösung:** Chrome im Inkognito-Modus öffnen (`Cmd + Shift + N`) und die HTTP-Adresse aufrufen.

## 3. WLAN-Konfiguration

- **SSID:** `router-parkit-pt`
    
- **WLAN-Passwort:** Im Passwortmanager hinterlegt
    
- **Router-Passwort:** Im Passwortmanager hinterlegt
    
- **Sicherheitsmodus:** WPA2 Personal
    
- **Verschlüsselung:** TKIP+AES (gemäss Screenshot)
    

## 4. Netzwerk und DHCP

- **Router-IP:** `192.168.1.1`
    
- **DHCP:** Aktiviert
    
- **Netzwerk:** `192.168.1.0/24`
    

Der Router vergibt automatisch IP-Adressen an verbundene Geräte.




### MCU

