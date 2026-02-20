# 📳 Android WiFi Power Commands (ADB + Linux)
This repository focuses on interacting directly with Android’s built-in Wi-Fi service via:

```
adb shell cmd wifi
```

It includes commands for:

* Inspecting Wi-Fi status and configuration
* Triggering scans and listing networks
* Connecting to open, WPA2, and hidden networks
* Managing saved networks
* Adjusting connection scoring
* Enabling verbose logging for debugging

This project is intended for educational, research, and lab use — ideal for developers, security researchers, and anyone interested in understanding how Android’s Wi-Fi stack works under the hood.

---

# ⚠️ Requirements

* Linux machine
* Android device with:

  * Developer Options enabled
  * USB Debugging enabled
* Android Debug Bridge (`adb`) installed

Install adb (Debian/Ubuntu):

```bash
sudo apt install adb
```

Verify connection:

```bash
adb devices
```

You should see your device listed.

---

# 📡 WiFi Command Walkthrough

All commands use:

```bash
adb shell cmd wifi <command>
```

---

# 1️⃣ Check WiFi Status

Check current WiFi state and connection info:

```bash
adb shell cmd wifi status
```

---

# 2️⃣ Enable / Disable WiFi

Enable WiFi:

```bash
adb shell cmd wifi set-wifi-enabled enabled
```

---

# 3️⃣ Get Country Code

Returns the regulatory country code currently applied:

```bash
adb shell cmd wifi get-country-code
```

---

# 4️⃣ Trigger a WiFi Scan

Force a scan:

```bash
adb shell cmd wifi start-scan
```

---

# 5️⃣ List Scan Results

View nearby networks from the last scan:

```bash
adb shell cmd wifi list-scan-results
```

---

# 6️⃣ Enable Scan Always Available

Allows scanning even when WiFi is turned off:

```bash
adb shell cmd wifi set-scan-always-available enabled
```

Verify:

```bash
adb shell cmd wifi status
```

---

# 7️⃣ List Saved Networks

Show saved network profiles:

```bash
adb shell cmd wifi list-networks
```

Example output:

```
0  MyNetwork
1  OfficeWiFi
```

---

# 8️⃣ Connect to a Network

### Connect to a standard WPA2 network:

```bash
adb shell cmd wifi connect-network "LabSSID" wpa2 "Password123"
```

### Connect to a hidden network:

```bash
adb shell cmd wifi connect-network "HiddenSSID" wpa2 "Password123"
```

### Connect to a specific BSSID (MAC address):

```bash
adb shell cmd wifi connect-network "LabSSID" wpa2 "Password123" -b aa:bb:cc:dd:ee:ff
```

---

# 9️⃣ Forget a Saved Network

First list networks:

```bash
adb shell cmd wifi list-networks
```

Then forget by ID:

```bash
adb shell cmd wifi forget-network 0
```

---

# 🔟 Connected Score Manipulation

⚠️ Requires active WiFi connection.

Set connection score (influences system network ranking):

```bash
adb shell cmd wifi set-connected-score 10
```

Reset score:

```bash
adb shell cmd wifi reset-connected-score
```

---

# 1️⃣1️⃣ SoftAP (Hotspot) Feature Support

Check supported hotspot capabilities:

```bash
adb shell cmd wifi get-softap-supported-features
```

---

# 1️⃣2️⃣ Verbose Logging (Advanced Debugging)

Check if verbose logging is enabled:

```bash
adb shell cmd wifi is-verbose-logging
```

Enable verbose logging (level 1):

```bash
adb shell cmd wifi set-verbose-logging enabled -l 1
```

Disable verbose logging:

```bash
adb shell cmd wifi set-verbose-logging disabled -l 0
```

Verify:

```bash
adb shell cmd wifi is-verbose-logging
```

---

# 🔬 Example Workflow

Example full workflow:

```bash
adb shell cmd wifi set-wifi-enabled enabled
adb shell cmd wifi start-scan
adb shell cmd wifi list-scan-results
adb shell cmd wifi connect-network "LabSSID" wpa2 "Password123"
adb shell cmd wifi status
```

---

# 🛠 Troubleshooting

If commands fail:

* Ensure device is authorized (`adb devices`)
* Make sure WiFi is enabled
* Some commands may require:

  * Root access
  * Specific Android versions
  * Active connection

---

# 📌 Notes

* These commands interact directly with Android's WiFi service.
* Behavior may vary depending on Android version and OEM modifications.
* Use responsibly and only on devices you own or have permission to test.

---

# 📜 License

For educational and research purposes only.

---

# ☕ Support This Project

If **AndroidWiFiCommands™** helps you in your understanding & exploration of Android devices, consider supporting ongoing development:

<p align="center">
  <a href="https://www.buymeacoffee.com/dfreshZ" target="_blank"><img src="https://cdn.buymeacoffee.com/buttons/v2/default-yellow.png" alt="Buy Me A Coffee" style="height: 60px !important;width: 217px !important;" ></a>
</p>

<!-- 
 _____              _       _____                        _          
|  ___| __ ___  ___| |__   |  ___|__  _ __ ___ _ __  ___(_) ___ ___ ™️
| |_ | '__/ _ \/ __| '_ \  | |_ / _ \| '__/ _ \ '_ \/ __| |/ __/ __|
|  _|| | |  __/\__ \ | | | |  _| (_) | | |  __/ | | \__ \ | (__\__ \
|_|  |_|  \___||___/_| |_| |_|  \___/|_|  \___|_| |_|___/_|\___|___/
        freshforensicsllc@tuta.com Fresh Forensics, LLC 2026 -->
