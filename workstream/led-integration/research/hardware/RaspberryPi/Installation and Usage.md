# PARKIT Orchestrator — Installation and Usage

This guide explains how the PARKIT Orchestrator was installed, how to connect to it, and how to run code. The Raspberry Pi runs without a screen, keyboard, or desktop interface.

## 1. System details

| Item | Value |
|---|---|
| Hostname | `PARKIT-Orchestrator` |
| Local network address | `parkit-orchestrator.local` |
| Username | `parkit-orchestrator` |
| Password | Stored in the team password manager; **not in GitHub** |
| Operating system | Raspberry Pi OS Lite (64-bit), Debian 13 (Trixie) |
| CPU architecture | `aarch64` |
| Memory | 8 GB (about 7.6 GiB usable) |
| Python | 3.13.5 |
| Remote access | SSH with password authentication |
| Wi-Fi network (SSID) | `router-parkit-pt` |
| Time zone | `Europe/Zurich` |
| Keyboard | Swiss (`ch`) |



## 2. What you need

- Raspberry Pi, power supply, and microSD card (32 GB used here)
- SD card reader and a Mac or another computer
- Raspberry Pi Imager (version 2.0.12 used here)
- PARKIT Wi-Fi router with SSID `router-parkit-pt`

Download Raspberry Pi Imager: https://www.raspberrypi.com/software/

## 3. Install the operating system

### Step 1 — Select the OS

Open Raspberry Pi Imager. Select the **actual** Raspberry Pi model. Choose **Raspberry Pi OS Lite (64-bit)**. Lite does not have a desktop interface, so it uses fewer resources.

![Raspberry Pi OS Lite selected](img/01-select-operating-system.png)

### Step 2 — Select the SD card

Select the microSD card. In this setup it appeared as **Generic USB SD Reader Media — 31.9 GB**.

> **Warning:** Writing the OS will erase the selected card.

![SD card selected](img/02-select-sd-card.png)

### Step 3 — Set the hostname

In **Customisation**, enter `PARKIT-Orchestrator` as the hostname.

![Hostname setup](img/03-set-hostname.png)

### Step 4 — Set the region

Use **Bern, Switzerland**, time zone **Europe/Zurich**, and keyboard layout **ch**.

![Region settings](img/04-set-region.png)

### Step 5 — Create the user

Set the username to `parkit-orchestrator`. Create a strong password and save it in the team password manager.

![User account setup with password hidden](img/05-create-user.png)

### Step 6 — Set up Wi-Fi

Choose **Secure Network** and set the Wi-Fi name (SSID) to **`router-parkit-pt`**. Enter the router Wi-Fi password from the team password manager. Leave **Hidden SSID** off unless the router network is hidden.

![Wi-Fi configuration screen (check the SSID against the current router settings)](img/06-wifi-settings.png)


### Step 7 — Enable SSH

Turn on **Enable SSH** and choose **Use password authentication** for the first setup.

![SSH enabled](img/08-enable-ssh.png)

### Step 8 — Optional: Raspberry Pi Connect

Raspberry Pi Connect was enabled in Imager. It requires internet access. For a local network without internet, use SSH instead. Raspberry Pi OS Lite supports remote shell access, not desktop screen sharing.

![Raspberry Pi Connect setup with token hidden](img/09-raspberry-pi-connect.png)

### Step 9 — Write the card

Complete the setup, write the OS to the card, wait for verification, and safely eject the card.

## 4. Start the Pi without a monitor

1. Make sure the Wi-Fi router `router-parkit-pt` is powered on.
2. Connect your Mac to the `router-parkit-pt` Wi-Fi network.
3. Insert the microSD card into the Pi.
4. Connect a suitable power supply and wait a few minutes for the first boot.
5. Open **Terminal** on the Mac.

Connect with SSH:

```bash
ssh parkit-orchestrator@parkit-orchestrator.local
```

On the first connection, check the host key fingerprint against a trusted value before accepting it. Enter the Linux password when asked. The password will not appear while typing.

![Successful SSH login](img/10-ssh-login.png)

If `.local` does not work, find the Pi's IP address in the router's connected-device list and use:

```bash
ssh parkit-orchestrator@<PI_IP_ADDRESS>
```

If SSH cannot connect, check that both devices are on `router-parkit-pt` and that the router does not have client isolation enabled.

## 5. Change system settings

Once connected by SSH, open the configuration menu:

```bash
sudo raspi-config
```

Use the arrow keys, Tab, and Enter to navigate. You can change system settings, interfaces, and regional settings. Some changes need a reboot.

![Raspberry Pi configuration menu](img/11-raspi-config.png)

Useful commands:

```bash
hostname                 # Show hostname
hostname -I              # Show local IP addresses
nmcli device wifi list   # List nearby Wi-Fi networks
nmcli connection show    # Show saved connections
sudo reboot              # Restart
sudo shutdown -h now     # Shut down safely
```

**Be careful:** Changing the active Wi-Fi connection may disconnect SSH.

## 6. Check that the Pi works

Run these commands in the SSH terminal:

```bash
cat /etc/os-release       # OS version
uname -m                  # CPU architecture
free -h                   # RAM usage
vcgencmd measure_temp     # CPU temperature
python3 --version         # Python version
cat /proc/device-tree/model  # Actual Pi model
```

Results shown in the setup screenshots:

- Debian GNU/Linux 13 (Trixie), Debian 13.7
- `aarch64` (64-bit ARM)
- About 7.6 GiB RAM total; about 235 MiB used at the time
- Temperature: 37.0°C at the time
- Python 3.13.5

![System test output](img/12-system-checks.png)

These checks show that the OS runs, SSH works, and Python is available. The screenshots do **not** confirm that a custom Python script has already been run.

## 7. Run your first Python script

Create a project folder:

```bash
mkdir -p ~/projects/hello
cd ~/projects/hello
nano test.py
```

Paste this code:

```python
import time

for i in range(3):
    print(f"PARKIT Orchestrator: test {i + 1}")
    time.sleep(1)

print("Test complete")
```

Save in `nano` with **Ctrl+O**, Enter, then **Ctrl+X**. Run:

```bash
python3 test.py
```

To create a virtual environment for a Python project:

```bash
cd ~/projects/hello
python3 -m venv .venv
source .venv/bin/activate
```

If the `venv` package is missing, it may need to be installed when internet or a package source is available.

## 8. Copy code from your Mac to the Pi

Run this on the **Mac**, not inside the SSH session:

```bash
scp ./test.py parkit-orchestrator@parkit-orchestrator.local:~/projects/hello/
```

Then connect to the Pi and run the file:

```bash
ssh parkit-orchestrator@parkit-orchestrator.local
cd ~/projects/hello
python3 test.py
```

For larger projects, use Git when network access and Git are available. Do not put passwords or tokens in the repository.

## 9. Stop or restart the Pi

```bash
sudo reboot            # Restart the Pi
sudo shutdown -h now   # Shut down safely
```

Wait until shutdown is complete before unplugging the power.