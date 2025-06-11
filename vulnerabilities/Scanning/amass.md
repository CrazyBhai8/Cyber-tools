# Amass - Subdomain Enumeration Tool 🕵️‍♂️

## 📌 What is Amass?
**Amass** is an open-source tool for **network mapping and attack surface discovery**. It is widely used by **penetration testers and security researchers** to find subdomains, IP addresses, and related network assets.

## 🚀 Why Use Amass?
- **Automatic subdomain discovery**
- **Uses OSINT, active scanning, and DNS enumeration**
- **Helps in bug bounty hunting & penetration testing**
- **Finds attack vectors in a target’s infrastructure**

## 🛠️ Installation
### Linux & Mac:
```bash
sudo apt install amass  # Debian-based systems (Ubuntu, Kali, etc.)
brew install amass  # Mac (Homebrew)
```
### Windows:
Download from [Amass GitHub](https://github.com/OWASP/Amass) and extract it.

---

## 🔎 Basic Amass Commands

### 1️⃣ Find Subdomains
```bash
amass enum -d example.com
```
Finds subdomains using passive enumeration.

### 2️⃣ Active Scanning (Aggressive)
```bash
amass enum -active -d example.com
```
Uses active techniques like DNS resolution.

### 3️⃣ Brute Force Subdomains
```bash
amass enum -brute -d example.com
```
Dictionary-based brute force for hidden subdomains.

### 4️⃣ Show Data Sources Used
```bash
amass enum -src -d example.com
```
Displays OSINT sources used to collect data.

### 5️⃣ Save Results to a File
```bash
amass enum -d example.com -o output.txt
```
Saves findings to `output.txt`.

### 6️⃣ Find ASN (Autonomous System Numbers) for a Company
```bash
amass intel -org "Company Name"
```
Useful for corporate reconnaissance.

### 7️⃣ Map Attack Surface
```bash
amass viz -d3 -d example.com -o graph_output.json
```
Creates a graph of discovered domains.

---

## 🔄 Amass Workflow in Cybersecurity
1️⃣ **Passive Scanning** – Collect information without interacting with the target.  
2️⃣ **Active Scanning** – Use brute force, DNS transfers, and certificate scraping.  
3️⃣ **Vulnerability Mapping** – Identify weak points in the system.  

---

## 🔗 Official Documentation  
For more details, visit the [Amass GitHub Repository](https://github.com/OWASP/Amass).

