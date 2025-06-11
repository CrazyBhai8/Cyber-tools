## 📌 What is Subfinder?
**Subfinder** is a fast and efficient subdomain enumeration tool used for reconnaissance. It mainly focuses on **passive enumeration**, making it **stealthy and faster** than other tools.

## 🚀 Why Use Subfinder?
- **Faster than Amass** for passive subdomain discovery.
- **Uses OSINT sources** like Shodan, Censys, VirusTotal.
- **No direct interaction with the target** (stealth mode).
- **Works well with other tools** like Amass, Nmap, and HTTPx.

## 🛠️ Installation
### Linux & Mac:
```bash
sudo apt install subfinder  # Debian-based systems (Ubuntu, Kali, etc.)
brew install subfinder  # Mac (Homebrew)
```
### Windows:
Download from [Subfinder GitHub](https://github.com/projectdiscovery/subfinder) and extract it.

## 🔑 Tip: Add API keys in ~/.config/subfinder/config.yaml for better results.

## 🔎 Basic Subfinder Commands

### 1️⃣ Find Subdomains of a Target
```bash
subfinder -d example.com
```
Finds subdomains using passive OSINT sources.

### 2️⃣ Save Results to a File
```bash
subfinder -d example.com -o results.txt
```
Saves the discovered subdomains to `results.txt`.

### 3️⃣ Use Specific Data Sources
```bash
subfinder -d example.com -sources virustotal,shodan
```
Queries only **VirusTotal** and **Shodan** for subdomains.

### 4️⃣ Recursive Subdomain Enumeration
```bash
subfinder -d example.com -recursive
```
Finds subdomains of already discovered subdomains.

### 5️⃣ Find Subdomains for Multiple Domains
```bash
subfinder -dL domains.txt -o results.txt
```



---

## 🔄 Subfinder Workflow in Cybersecurity
1️⃣ **Passive Subdomain Collection** – OSINT-based reconnaissance.  
2️⃣ **Filter & Analyze Data** – Extract useful subdomains.  
3️⃣ **Combine with Active Tools** – Use Amass, Nmap, etc. for deeper analysis.  
4️⃣ **Test Discovered Subdomains** – Check for vulnerabilities and live hosts.

---

## 🔗 Official Documentation  
For more details, visit the [Subfinder GitHub Repository](https://github.com/projectdiscovery/subfinder).

