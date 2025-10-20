- Last resort to gain access to a WPA/WPA2 network.
- Relies on social engineering.

Idea:
1. Start a fack AP with same name as target network.
2. Disconnect a client.
3. Wait for them to connect to the fack AP.
4. Automatically display a page asking for network key.

Advantaqe - no need for guessing.
Drawbacks:
1. User have to connect to open fack AP.
2. They have to enter their WPA key in a web page.

---
# 🧠 Evil Twin Attack (Manual & Automatic Using Fluxion)

---

## 🧩 1. Concept Overview

* When all technical attacks (wordlist, WPS exploit, etc.) fail → **target the users**.
* The **Evil Twin Attack** tricks users into connecting to a **fake access point (AP)** that looks identical to their real one.

---

## ⚙️ 2. Attack Logic

1. **Create a fake AP** (same SSID as the target Wi-Fi).
2. **Deauthenticate** all users from the real AP (so they’ll reconnect to yours).
3. **Host a fake login page** asking for the Wi-Fi password (WPA key).
4. **Victim enters password → attacker captures it.**

---

## 🧠 3. Why It Works

✅ No brute-force needed — the user types the real password.
✅ Works even with strong passwords.

---

## ⚠️ 4. Drawbacks / Risks

* Users must connect to an **open (unsecured)** network → may raise suspicion.
* Login page opens in browser — some may realize it’s fake.
* More believable on **phones/macOS** (page shown inside a system popup) than on **Windows/Linux** (opens in browser).

---

## 📶 5. Difference from Captive Portal Attack

| Captive Portal             | Evil Twin                            |
| -------------------------- | ------------------------------------ |
| Users expect login page    | Users don’t expect login page        |
| Network is open by default | Original WPA/WPA2 network is secured |
| Easier to fool users       | More suspicious setup                |

---

## 🧰 6. Manual Evil Twin Steps

1. **Prepare fake AP:**

   * Same SSID as target.
   * Open network (no password).

2. **Start required services:**

   * `airbase-ng` → create fake AP
   * `dnsmasq` → DNS spoofing
   * `apache2` → host fake login page

3. **Disconnect users** from real AP using deauth attack.

4. **Fake login page options:**

   * Create one yourself (HTML form).
   * Download ready-made template.
   * Use **router’s admin login page** (most convincing).

5. **Modify the HTML page:**

   * Remove username field.
   * Replace login prompt with:
     👉 *“Please enter your Wi-Fi password to reconnect.”*

6. **Collect submitted credentials** from web server logs.

---

## 🧮 7. How to Get Router Login Page

* Find router IP:

  ```bash
  route -n
  ```
* Usually → `192.168.1.254` or similar.
* Open it in browser → copy the HTML login page.
* Edit it as your fake WPA login prompt.

---

## ⚡ 8. Automating with Fluxion

Instead of doing everything manually, use **Fluxion** — a tool that automates the entire Evil Twin process.

### 🔧 What Fluxion Does Automatically

* Scans for target networks
* Creates fake AP (same SSID)
* Launches web server + DNS
* Displays fake login template
* Deauthenticates users from real AP
* Validates password entered by victim

---

## 🧩 9. Installing Fluxion (v2 preferred)

[Fluxion](https://github.com/FluxionNetwork/fluxion.git)

```bash
cd /opt
git clone https://github.com/FluxionNetwork/fluxion.git
cd fluxion/install
bash install.sh
```

* Installs dependencies automatically.
* **Fluxion 2** recommended (more stable, better templates)
* Fluxion 3 exists but is **buggy** and has fewer templates.

---

## 🚀 10. Running Fluxion

```bash
cd /opt/fluxion
bash fluxion.sh
```

* Follow the guided menu:

  1. Select target network
  2. Choose attack type → *Fake AP*
  3. Pick login page template
  4. Start attack

Fluxion will:

* Create fake AP
* Deauth real users
* Show fake login page
* Capture WPA key entered
* Verify if password is valid

---

## 💡 11. Why Learn Manual First?

* You understand how Wi-Fi APs, DHCP, DNS, and web redirects work.
* You can **adapt the attack** for other use cases (e.g., captive portals).
* If Fluxion fails or has bugs → you can perform it manually.

✅ **Evil Twin = Social Engineering + Wi-Fi Spoofing**
⚡ **Fluxion = Automates Everything (but manual knowledge is power!)**


--- 
# 🧠  Using **Fluxion** for an Automatic Evil Twin Attack

---

## ⚙️ 1. Purpose

Fluxion automates the **Evil Twin attack** — it creates a fake Wi-Fi network identical to the target’s and tricks users into entering their WPA/WPA2 password through a fake login page.

---

## 🧩 2. Setup & Launch

### Step 1: Navigate to the tool’s directory

```bash
cd /opt/fluxion
```

### Step 2: Run the script

```bash
bash fluxion.sh
```

---

## 🌐 3. Configuration Steps (Interactive Setup)

### 🗣️ a. Language

* Select your language (e.g., **1 → English**).

### 📡 b. Channel Scan

* Choose **All Channels (1)** to discover all available networks.

Fluxion will automatically open **Airodump-ng** to list nearby Wi-Fi networks.

### 🎯 c. Select Target

* Find your target (e.g., `UPC Network`)
* Note its ID and enter that number (e.g., **3**).

---

## 🧱 4. Fake Access Point Creation

Fluxion asks which tool to use:

* **1 → Hostapd** (recommended, stable)
* **2 → Airbase-ng**

➡️ Choose **1 (Hostapd)** to generate the fake access point.

---

## 🪪 5. Handshake (Verification Step)

Fluxion can:

* Use an existing **.cap** handshake file
  (e.g., `/root/handshake01.cap`)
* Or **capture one automatically** if you skip (press *Enter*).

Fluxion verifies the handshake using **Pyrit** or **Aircrack-ng**.

---

## 🔐 6. SSL Certificate

Prompt:

> Create or search for an SSL certificate?

✅ Choose **1 – Create new certificate**
(to enable HTTPS on the fake login page)

---

## 🧰 7. Web Interface (Login Template)

Fluxion will display available templates:

* Generic (English, French, Arabic, etc.)
* Router-specific (TP-Link, Netgear, Belkin, Virgin Media, etc.)

👉 Pick the one matching the victim’s router brand for realism.

Example:
If target router is TP-Link → choose **option 33**.

---

## 🚀 8. Attack Deployment

Fluxion will now:

* Start **fake AP** (same SSID as target)
* Launch **DHCP & DNS servers**
* Start **web server** hosting the fake login page
* Run **deauth attack** to disconnect users from the real AP

Clients lose Wi-Fi connection → reconnect automatically to the fake AP.

---

## 📲 9. Victim Experience

* The victim sees their usual Wi-Fi name (SSID).
* They connect → a **login page** appears asking for the WPA key.
* The page may simulate:

  * Router firmware upgrade
  * Security verification
  * “Enter your Wi-Fi password to reconnect”

Once entered, Fluxion:

1. Captures the password.
2. Verifies it against the handshake.
3. Confirms if it’s valid.

---

## 🧪 10. Example Output

Fluxion confirms successful capture:

```
Password found: 1234abcd
Verified using Aircrack-ng
```

✅ Attack complete — the correct WPA2 key has been obtained.

---
# 🧠 Fixing Broken Login Pages in **Fluxion** (Relative URL Bug)

---

## ⚙️ 1. Problem Overview

When using **Fluxion**, sometimes the **auto-displayed login page** looks broken or suspicious.
✅ All other parts of the attack (DHCP, DNS spoofing, HTTPS, web server) work fine.
❌ Only the *first auto-popup page* fails to load CSS/JS styles.

---

## 🕵️ 2. Root Cause Analysis

* The page loads fine when directly visiting a URL like:

  ```
  http://example.com/index.html
  ```
* But it **breaks** when the browser adds folders after the domain:

  ```
  http://example.com/fwlink/somepath
  ```

🧩 **Reason:**
The login page uses **relative URLs** (e.g., `href="bootstrap.min.css"`) instead of **absolute URLs**.

When the browser sees a relative path, it tries to load the resource *relative to the current directory* (`fwlink/`), which doesn’t exist on the Fluxion web server.

---

## 🧰 3. Locating the Web Files

Fluxion stores all temporary files in `/tmp/fluxion/`.

### Navigate to the directory:

```bash
cd /tmp/fluxion
```

Inside, you’ll find:

* Web templates (`index.html`, `check.php`, etc.)
* Captured data
* Server configs for **Lighttpd** (not Apache)

---

## 🧾 4. Fixing the HTML Code

1. Open `index.html` (the main login page):

   ```bash
   sudo nano /tmp/fluxion/data/index.html
   ```

   *(You can also use Genie or any editor.)*

2. Find **relative paths**:

   ```html
   <link href="bootstrap.min.css" rel="stylesheet">
   <script src="main.js"></script>
   <form action="check.php">
   ```

3. Add a **forward slash (`/`)** before each path:

   ```html
   <link href="/bootstrap.min.css" rel="stylesheet">
   <script src="/main.js"></script>
   <form action="/check.php">
   ```

✅ This makes all paths **absolute from the webroot**, ensuring they load correctly regardless of directory.

---

## 🧮 5. Batch Fix Using Search & Replace

To quickly apply the fix inside your editor:

* For **CSS/JS links**:

  * Find: `href="`
  * Replace with: `href="/`

* For **script tags**:

  * Find: `src="`
  * Replace with: `src="/`

* For **form actions**:

  * Find: `action="`
  * Replace with: `action="/`

This converts all relative URLs into absolute ones.

---

## 💾 6. Save & Restart

After editing:

```bash
Ctrl + S  (Save)
Ctrl + Q  (Quit)
```

Then restart Fluxion’s web interface or re-run the attack.

---

## ✅ 7. Verification

Reconnect to your **Evil Twin** network:

* The auto-login popup now displays perfectly.
* Styles and scripts load correctly.
* The fake router upgrade/login page looks legit.

If the user enters their password → it’s captured and verified instantly by Aircrack-ng.

---

## 💡 8. Takeaways

| Problem                                  | Cause                              | Fix                           |
| ---------------------------------------- | ---------------------------------- | ----------------------------- |
| Broken auto-login page                   | Relative URLs                      | Add `/` to make URLs absolute |
| Files not found                          | Browser looking in wrong directory | Use webroot-based links       |
| Works on manual visit but not auto-popup | Different URL structure            | Fixed with absolute paths     |

---

## 🧠 Bonus Insight

This bug affects **all Fluxion templates**, not just TP-Link.
So apply the same fix to any template you use.

---

**Result:**
✨ The attack now appears professional and convincing — especially on mobile & macOS, where the popup opens in a native window, not a browser.

---