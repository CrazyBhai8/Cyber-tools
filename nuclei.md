# Nuclei Tool- Automated Scanner (Highly Customizable)

Absolutely! Let's break down **Nuclei** in a way that even a beginner can grasp. 🔍💥

---

### 🔧 What is Nuclei?

**Nuclei** is an open-source **vulnerability scanner** — a **tool that helps find security holes** (bugs, misconfigurations, etc.) in websites, apps, and systems.

Think of it like a robot hacker 👾 that runs pre-made scripts to **scan targets and report weaknesses**.

---

### 🧠 How Does It Work?

At the heart of Nuclei is something called **templates**. These are like instructions or "hacking recipes" for what to look for.

Each template tells Nuclei:

* What kind of bug to check for
* Where to check
* What the response should look like if the bug exists

Nuclei then:

1. Takes a list of targets (like `https://example.com`)
2. Loads a bunch of templates
3. Starts scanning 🚀
4. Reports what it finds (like **XSS**, **SQLi**, **open APIs**, **leaked secrets**, etc.)

---

### ⚡ Why is it Awesome?

* 🧠 **Highly customizable** – You can write your own templates.
* 💣 **Fast** – It can scan hundreds of targets per second.
* 🛠️ **Modular** – Use it in bug bounties, pentesting, recon, or automation.
* 📚 **Huge community** – Tons of pre-made templates from the security community.
* 🤖 **Automation-friendly** – Perfect for use in scripts, CI/CD, or recon pipelines.

---

### 📦 Real Example

You have a list of websites in `targets.txt`, and you want to check them for common misconfigurations. You run:

```bash
nuclei -l targets.txt -t cves/
```

Boom! 💥 It scans every target using CVE-based templates and shows you what vulnerabilities were found.

---

### 📁 Template Example (Simplified)

```yaml
id: basic-xss
info:
  name: Basic XSS
  severity: medium
requests:
  - method: GET
    path:
      - "{{BaseURL}}/?q=<script>alert(1)</script>"
    matchers:
      - type: word
        words:
          - "<script>alert(1)</script>"
```

This checks if a site reflects a `<script>` tag (i.e., possible **XSS**).

---

### 🧪 Use-Cases

* Bug bounty hunting 🏴‍☠️
* Web app pentesting 🔐
* Red team recon 🕵️‍♂️
* Automated security checks 🔄

---
### 🛠️ **Basic Command**

```bash
nuclei -u https://target.com
nuclei -l targets.txt -t cves/ -c 50
```

* Scans **one** URL with **default templates**.
- ADD -silent for **Silent Mode (Just Output Hits)**
* `-c 50` sets 50 concurrent threads. Speed boost ⚡ (but careful not to DDoS accidentally 😅).
- `nuclei -tl` list aviable tamplate


---

### 📜 **Scan Multiple Targets**

```bash
nuclei -l targets.txt
```

* `targets.txt` should contain one URL per line.

---

### 📁 **Use Specific Templates**

```bash
nuclei -u https://target.com -t vulnerabilities/
```

* Only scans using templates inside the `vulnerabilities/` directory.

---

### 💣 **Scan for CVEs (Common Vulnerabilities)**

```bash
nuclei -l targets.txt -t cves/
```

### 🧠 **Use Specific Template by ID**

```bash
nuclei -u https://target.com -tags xss
```

* Runs only templates tagged with `xss`.

---

### 🔒 **Authenticated Scanning (Header Support)**

```bash
nuclei -u https://target.com -H "Authorization: Bearer <your_token_here>"
```

Great question! 🔍 Choosing the **right Nuclei template** depends on **what you're targeting** and **your goal** (bug bounty, internal audit, misconfig scan, etc.). Let's break it down nice and simple. 🧠💡

---

## 🧬 **How to Choose Nuclei Templates**

| 🎯 Goal / Situation                      | 📁 Template Directory                             | 🔥 Use-case                                                         |
| ---------------------------------------- | ------------------------------------------------- | ------------------------------------------------------------------- |
| ✅ **Find known vulnerabilities (CVEs)**  | `cves/`                                           | Check for known bugs in outdated tech (e.g., Log4Shell, Struts RCE) |
| 🛠️ **Check for misconfigurations**      | `misconfiguration/`                               | Detect open admin panels, exposed `.git`, directory listing, etc.   |
| 🔐 **Test for exposed sensitive files**  | `exposures/`                                      | Look for `.env`, backup files, database dumps                       |
| 💥 **Look for RCE, LFI, SQLi, etc.**     | `vulnerabilities/`                                | Scan for high-severity issues                                       |
| 🧪 **Find XSS, SSRF, IDOR, etc.**        | `vulnerabilities/`, `workflows/`                  | Bug bounty style vuln hunting                                       |
| 🌍 **Check tech stack & fingerprinting** | `technologies/`                                   | Detect what tech the target uses (e.g., Apache, WordPress)          |
| 🛡️ **Test known web apps**              | `takeovers/`, `exposures/`, `default-logins/`     | Check for subdomain takeovers, default creds                        |
| 🧰 **Do recon-level scans**              | `dns/`, `network/`, `ssl/`, `generic-detections/` | Port scanning, DNS zone issues, SSL misconfigs                      |
| 📊 **Comprehensive bug bounty scan**     | `http/`, `default-credentials/`, `miscellaneous/` | Use full sets for wide recon sweeps                                 |

---

## 🧠 Pro Tips for Choosing Templates

* 📁 Use `-tags` to filter:

  ```bash
  nuclei -u https://target.com -tags xss,sqli
  ```

* 🧪 Use **workflows** for chained scans (auto decision-based):

  ```bash
  nuclei -u https://target.com -w workflows/
  ```

* 🔍 Find template categories:

  ```bash
  nuclei -tl
  ```

* 🔎 Search for specific vuln by name:

  ```bash
  nuclei -t cves/ | grep log4j
  ```

---

## 🛠 Sample Use Case

**Scenario**: You’re hunting for bugs on a target running WordPress.

### Recommended templates:

```bash
-t cves/ -t vulnerabilities/ -t exposures/ -t misconfiguration/
```

**Plus**:

```bash
-tags wordpress
```

---

## 👇 TL;DR Decision Tree

1. **Bug Bounty** ➜ `vulnerabilities/`, `cves/`, `misconfiguration/`
2. **Internal Pentest** ➜ Add `default-logins/`, `ssl/`, `network/`
3. **Recon/Discovery** ➜ `technologies/`, `dns/`, `generic-detections/`
4. **Subdomain Takeover** ➜ `takeovers/`

