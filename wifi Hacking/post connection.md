
# 🧠 Post-Connection Attacks Overview

## 🔹 What are Post-Connection Attacks?

* Attacks performed **after connecting** to a target network (Wi-Fi or wired).
* Work on **both** wireless and wired networks.
* Require that you are **connected** to the same network/subnet.

---

## 🔹 Section Structure

### 1. **Manual ARP Spoofing & MITM Basics**

* Learn to perform **ARP spoofing** manually.
* Become **Man-in-the-Middle (MITM)**.
* Perform:

  * Data sniffing
  * HTTP/HTTPS bypass
  * DNS spoofing
  * HTML/JS code injection
* Understand how tools like `mitmproxy`, `Ettercap`, or `Bettercap` automate these steps.

**Why manually?**

* If scripts fail, you can fix or debug them.
* Lets you reuse components for your own custom attacks.
* Builds a deeper understanding of what’s happening under the hood.

---

### 2. **Analyzing Data Flows & Building Custom Attacks**

* Learn to **analyze** what happens when users interact with the network.
* Steps:

  1. Observe network behavior (what triggers what?).
  2. Identify potential attack points.
  3. Build the logic of the attack.
  4. Implement it manually.
* Example manual attacks:

  * Injecting JavaScript
  * Modifying HTML code before delivery

Goal → become independent of existing tools.

---

### 3. **Writing Your Own Attack Scripts**

* Learn to:

  * **Conceptualize**, **develop**, and **automate** your own attacks.
  * Write scripts to execute your logic.
* Build unique tools that **don’t yet exist** publicly.
* You’ll gain the ability to take an idea and **turn it into a working exploit/tool**.

**Example project:**

* Build a tool that turns any file downloaded over the network into a **Trojan** (for lab/testing).

---

## 🔹 Skills & Outcomes

By the end of the section:

* You can run **ARP spoofing** manually.
* Perform **MITM**, sniff data, modify packets.
* Bypass **router security features** (like ARP protection).
* Create and test your **own custom attacks**.
* Write scripts to **automate** them.

---

## 🔹 Why This is Crucial

* Tools automate attacks but also hide the logic.
* Manual knowledge lets you:

  * Understand failures.
  * Build **new, creative** attacks.
  * Adapt to **unique environments**.
* This skill is what separates **script kiddies** from **ethical hackers** or **researchers**.

---

# 🧠 Ettercap Overview & Basic Usage

## 🔹 What is Ettercap?

* **Ettercap** is a **Man-in-the-Middle (MITM) framework**.
* Allows you to run multiple MITM attacks easily.
* Includes:

  * Built-in **sniffer**
  * Support for **plugins**
  * Tools for **ARP spoofing**, **packet capture**, and **data manipulation**

---

## 🔹 Why Use Ettercap?

* It’s a **simpler**, more **reliable** alternative to *mitmproxy* or *Bettercap*.
* Useful if you experience issues with **mitmproxy/man-in-the-middle frameworks**.
* Can perform **the same attacks**: sniffing, spoofing, injecting, etc.
* Comes **preinstalled** in **Kali Linux**.

---

## 🔹 Preparing Ettercap for Use

### 1. Modify Configuration File

Path:

```bash
/etc/ettercap/etter.conf
```

Steps:

1. Open with `leafpad` or `nano`:

   ```bash
   leafpad /etc/ettercap/etter.conf
   ```
2. Find lines related to:

   * `IPChains`
   * `IPTables`
3. **Uncomment** (remove `#`) the lines under **IPTables** (since we use that).
4. Set both **UID** and **GID** to **0** (root):

   ```bash
   ec_uid = 0
   ec_gid = 0
   ```
5. Save (`Ctrl + S`) and exit (`Ctrl + Q`).

✅ This prevents warnings and ensures Ettercap runs with full privileges.

---

## 🔹 Basic Syntax

```bash
ettercap [options] [targets]
```

Examples:

* View help:

  ```bash
  ettercap --help
  ```

### General format:

```
ettercap [OPTIONS] [TARGET1] [TARGET2]
```

You can use:

* `-t` or `--text` → Text mode
* `-T` (capital) → Text mode with interface
* `-q` → Quiet mode (no extra output)

---

## 🔹 User Interfaces in Ettercap

| Mode | Description                            |
| ---- | -------------------------------------- |
| `-T` | Text interface (used most often)       |
| `-G` | Graphical GTK interface                |
| `-D` | Daemon/background mode                 |
| `-C` | Curses-based (interactive terminal UI) |

> The instructor prefers **text mode (quiet)** because it’s faster and simpler.

---

## 🔹 Running Ettercap (Basic Command)

Command used in demo:

```bash
ettercap -Tq ///
```

Explanation:

* `-T` → Text interface
* `-q` → Quiet output
* `///` → No targets specified (just scan for connected hosts)

Ettercap will:

* **Scan** the network automatically.
* **List** connected hosts (like `netdiscover`).

---

## 🔹 Interactive Text Mode Commands

Once running, press these keys:

| Key | Function                           |
| --- | ---------------------------------- |
| `h` | Help – list all available commands |
| `l` | List connected hosts (IPs & MACs)  |
| `p` | Print profiles                     |
| `c` | Print connections                  |
| `s` | Show interfaces                    |
| `f` | Activate filters                   |
| `p` | Activate plugins                   |
| `q` | Quit program                       |

Example:

* Press `l` to list connected devices (similar to `netdiscover` output).

---

# 🧠 ARP Spoofing with Ettercap

## 🔹 Recap

* Previously: Learned Ettercap basics and how to list connected hosts.
* Now: Performing an **ARP Spoofing (Man-in-the-Middle)** attack using Ettercap.

---

## 🔹 Understanding the Setup

### ✅ Network Overview

* Target: Windows machine

  * IP → `10.22.15.9`
  * Gateway → `10.22.15.1`
* Attacker: Kali machine

  * Interface → `eth0` (or `eth0` equivalent)
  * IP → `10.22.15.8`

🧩 **Key rule:**
Both attacker and victim must be on the **same subnet** (e.g. `10.22.15.x`).

---

## 🔹 Command Structure

### Base Command:

```bash
ettercap -Tq -M arp:remote -i eth0 //10.22.15.1// //10.22.15.9//
```

### Breakdown:

| Option           | Meaning                            |
| ---------------- | ---------------------------------- |
| `-T`             | Text interface                     |
| `-q`             | Quiet mode                         |
| `-M arp:remote`  | Specify MITM method = ARP spoofing |
| `-i eth0`        | Interface to use                   |
| `//10.22.15.1//` | Group 1 = Gateway                  |
| `//10.22.15.9//` | Group 2 = Target                   |

🧠 You can reverse the order — as long as gateway and target are in **separate groups**.

---

## 🔹 Target & Group Rules

* Ettercap requires **two groups**:

  * Group 1 = one endpoint (e.g. router)
  * Group 2 = other endpoint (e.g. victim)
* Formats:

  * Use `///` to target **all** hosts.
  * Use `//IP//` to specify one.
  * Use ranges like `10.22.15.9-20` to include multiple.
  * Use commas `10.22.15.9,10.22.15.10` to separate hosts.
* Fields (between slashes):

  * 1st → MAC address (optional)
  * 2nd → IP address (used most)
  * 3rd → IPv6 (optional)
  * 4th → Port (optional)

---

## 🔹 Steps Summary

1. **Check connectivity**

   ```bash
   ifconfig
   ```

   → Confirm same subnet as target.

2. **Run Ettercap ARP Spoofing**

   ```bash
   ettercap -Tq -M arp:remote -i eth0 //10.22.15.1// //10.22.15.9//
   ```

3. **Verify attack on victim**

   ```bash
   arp -a
   ```

   → The gateway MAC will now match the attacker’s MAC address.

4. **Sniffer starts automatically**

   * Ettercap listens for credentials sent over HTTP.

---

## 🔹 Example Result

When victim logs into a website (e.g. `dictionary.com`):

```
Username: test@mitm.org
Password: 123456
Page: login.dictionary.com
```

🎯 Ettercap captures and displays this in real-time.

---


# 🧠 Ettercap Plugins (Auto Add Example)

## 🔹 What are Ettercap Plugins?

* Ettercap includes **multiple plugins** to extend its capabilities.
* Plugins allow automation of various **Man-in-the-Middle** operations.
* Each plugin can be **activated or deactivated** while Ettercap runs.
* Plugins can:

  * Add new hosts dynamically
  * Modify captured data
  * Log sessions
  * Perform automated tasks during MITM attacks

---

## 🔹 Example Plugin: `autoadd` (Auto Add Hosts)

### 🧩 Purpose

* Automatically **adds new hosts** to the poisoned target list.
* Useful when targeting an **entire subnet**.
* Without it → new devices joining after attack start **won’t be poisoned**.
* With it → new devices automatically **get added & poisoned**.

---

## 🔹 Lab Setup Summary

* Attack run against a **real Wi-Fi network** (not virtual).
* Wireless adapter connected via USB.
* Interface in use: `wlan0` (instead of `eth0`).
* Target (Windows) initially **disconnected**, then connected after attack started.

---

## 🔹 Command Used

```bash
ettercap -Tq -M arp:remote -i wlan0 ///
```

### Breakdown

| Option          | Meaning                               |
| --------------- | ------------------------------------- |
| `-T`            | Text interface                        |
| `-q`            | Quiet mode                            |
| `-M arp:remote` | ARP spoofing method                   |
| `-i wlan0`      | Wireless interface                    |
| `///`           | Targets the entire subnet (all hosts) |

---

## 🔹 Checking Current Hosts

After starting Ettercap:

* Press `h` → help menu
* Press `l` → lists current poisoned hosts

  * Shows IPs currently under MITM
  * Initially includes only devices **connected before** the attack started

---

## 🔹 Listing & Activating Plugins

1. Press `p` → List all available plugins

   * `0` = inactive
   * Displays plugin name, version, and description

2. Locate `autoadd` plugin:

   ```
   autoadd — automatically add new victims to target range
   ```

3. Activate it:

   ```
   autoadd
   ```

4. Ettercap responds:

   ```
   Activating autoadd plugin...
   ```

✅ Now, whenever a new host connects, Ettercap automatically adds and poisons it.

---

## 🔹 Demo Summary

1. Attacker runs Ettercap with `autoadd`.
2. Victim connects to Wi-Fi **after** the attack starts.
3. Ettercap outputs:

   ```
   Added new host: 192.168.2.3
   ```
4. Press `l` again — new IP appears in list.
5. Ettercap begins intercepting and sniffing packets automatically.

---

## 🔹 Proof of Success

* Victim logs in to `dictionary.com`.
* Ettercap sniffer captures credentials instantly.
* Confirms MITM + plugin functionality are working.

---

## 🔹 Why `autoadd` is Useful

* Ensures **continuous coverage** of all clients in subnet.
* Prevents missing out on new connections.
* Ideal for **broad network attacks** or dynamic environments (e.g., public Wi-Fi).

---

# 🧠 Notes — Ettercap Plugin: DNS Spoof

## 🔹 Purpose

* The **DNS spoof plugin** lets you **redirect DNS requests** to any IP address.
* Example: Redirect `bing.com` → your own local web server.
* Common uses:

  * Fake login pages
  * Phishing tests
  * Malware delivery
  * Serving fake software updates

---

## 🔹 How It Works

* DNS spoofing changes where a target’s **browser is sent** when they request a domain.
* The attacker tells the victim that a domain (e.g., `bing.com`) → attacker’s IP.
* When the victim visits the site, they are served **a fake page** from the attacker’s machine.

---

## 🔹 Step 1: Configure DNS Rules

1. Open the Ettercap DNS configuration file:

   ```bash
   leafpad /etc/ettercap/etter.dns
   ```

2. Scroll to the records section and add your spoofing rules:

   ```bash
   bing.com      A   192.168.2.5
   *.bing.com    A   192.168.2.5
   ```

   * `A` → DNS record type (maps domain → IP)
   * `192.168.2.5` → your **attacker machine IP**

3. You can use `*` as a wildcard for **all subdomains**.

4. Verify your attacker IP:

   ```bash
   ifconfig
   ```

---

## 🔹 Step 2: Start a Web Server

Since victims will be redirected to your computer:

```bash
service apache2 start
```

This ensures they see your fake webpage hosted locally.

---

## 🔹 Step 3: Run Ettercap with DNS Spoof Plugin

Example command:

```bash
ettercap -Tq -M arp:remote -i wlan0 -s -P dns_spoof //192.168.2.3// //192.168.2.1//
```

### Breakdown:

| Option            | Meaning                               |
| ----------------- | ------------------------------------- |
| `-T`              | Text mode                             |
| `-q`              | Quiet output                          |
| `-M arp:remote`   | ARP spoofing MITM method              |
| `-i wlan0`        | Wireless interface                    |
| `-s`              | Disable self-signed SSL cert creation |
| `-P dns_spoof`    | Activate DNS spoof plugin             |
| `//192.168.2.3//` | Victim target                         |
| `//192.168.2.1//` | Gateway (router)                      |

> ✅ Tip:
> You can **activate plugins directly in the command** using `-P` instead of typing `p` inside Ettercap.

---

## 🔹 Step 4: Verify Attack

* On victim machine, open:

  ```
  bing.com
  ```
* The browser will load **your fake site** from your Apache server.
* Ettercap will display messages like:

  ```
  Activating dns_spoof plugin
  ```

---

## 🔹 Why DNS Spoofing is Powerful

* Works on both **wired and wireless** networks.
* Can be combined with:

  * Fake updates
  * Trojan downloads
  * Credential harvesting pages
* Bypasses normal URL filtering if DNS responses are trusted.

---
# 🧠  Ettercap One-Way Spoofing

## 🔹 Concept Recap: ARP Spoofing

* In a typical **Man-in-the-Middle (MITM)** attack:

  * The hacker poisons both **victim** and **router** ARP tables.
  * Victim thinks hacker = router.
  * Router thinks hacker = victim.
  * All data flows through the hacker — **requests and responses**.
* This allows:

  * Full data capture.
  * Data manipulation (injecting code, altering pages).

---

## 🔹 Problem: Detection by Routers

* Some routers/gateways have **anti-ARP-spoofing defenses**:

  * Use tools like **ARPwatch**, IDS/IPS systems.
  * Detect when **two IPs share the same MAC address**.
  * Raise alarms or **block** the attacker.
* Happens because the attacker’s MAC appears in both victim and router ARP entries.

---

## 🔹 Solution: One-Way Spoofing

* **Bypass ARP defenses** using one-way spoofing.
* Only **spoof the victim**, **not** the router.

### ⚙️ How It Works

1. Hacker tells victim:
   “I am the router” → victim sends all requests to hacker.
2. Hacker forwards requests → router → Internet.
3. Router sends responses **directly** back to victim.
4. Hacker can:

   * Sniff outgoing requests.
   * Capture URLs, usernames, passwords, DNS data.
5. Hacker **cannot**:

   * See return packets.
   * Modify content or inject code.

✅ **Result:**
No duplicate MAC entries in router ARP table → avoids detection.

---

## 🔹 Command Example

```bash
ettercap -Tq -M arp:oneway -i eth0 -s //10.0.2.9// //10.0.2.1//
```

### Breakdown

| Option          | Description              |
| --------------- | ------------------------ |
| `-T`            | Text mode                |
| `-q`            | Quiet mode               |
| `-M arp:oneway` | One-way ARP spoofing     |
| `-i eth0`       | Interface to use         |
| `-s`            | Don’t generate SSL certs |
| `//10.0.2.9//`  | Victim IP                |
| `//10.0.2.1//`  | Router/Gateway IP        |

🧩 Important:

* Target **1** = Victim
* Target **2** = Router
* Packets only spoofed **from victim → router**.

---

## 🔹 Using Wireshark for Analysis

* Ettercap might **miss some credentials** during one-way spoofing.
* Solution: Run **Wireshark** on the same interface.

### Steps:

1. Start Wireshark:

   ```bash
   wireshark &
   ```
2. Choose correct interface (e.g., `eth0` or `wlan0`).
3. Set filter:

   ```
   http
   ```
4. Watch for **POST** requests to find:

   * Usernames
   * Passwords
   * Login URLs

---

## 🔹 Practical Example

* Victim logs into `dictionary.com`:

  * Username: `zayde@zsecurity.org`
  * Password: `123456`
* Wireshark captures credentials from HTTP POST.
* Ettercap’s sniffer **missed them**, but Wireshark displayed them.

---
