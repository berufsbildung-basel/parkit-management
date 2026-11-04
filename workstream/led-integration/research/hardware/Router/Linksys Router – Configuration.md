## 1. Router Information

- **Model:** Linksys WRT54GL (Wireless-G 2.4 GHz)

- **Firmware:** v4.30.11

- **Gateway:** `192.168.1.1`

- **Router IP:** `192.168.1.1`


## 2. Accessing the Router Settings

**URL:** [http://192.168.1.1](http://192.168.1.1/)

- **Username:** `admin`

- **Password:** https://vault-amer.adobe.net/ui/vault/secrets-engines/kv2_parkit/kv/team%2FRouter_Prototype


**Problem:** The following errors occurred when attempting to access the settings normally via Chrome:

- `400 Bad Request`

- `ERR_SSL_VERSION_OR_CIPHER_MISMATCH`


**Solution:** Open Chrome in Incognito mode (`Cmd + Shift + N`) and enter the HTTP address.

## 3. Wi-Fi Configuration

- **SSID:** `router-parkit-pt`

- **Wi-Fi Password:** https://vault-amer.adobe.net/ui/vault/secrets-engines/kv2_parkit/kv/team%2FRouter_Prototype
##### 4. Netzwerk und DHCP

- **Router Password:** https://vault-amer.adobe.net/ui/vault/secrets-engines/kv2_parkit/kv/team%2FRouter_Prototype

- **Security Mode:** WPA2 Personal

- **Encryption:** TKIP+AES (as shown in the screenshot)


## 4. Network and DHCP

- **Router IP:** `192.168.1.1`

- **DHCP:** Enabled

- **Network:** `192.168.1.0/24`


The router automatically assigns IP addresses to connected devices.
