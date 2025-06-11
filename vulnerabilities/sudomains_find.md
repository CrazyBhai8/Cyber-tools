
## subfinder

subfinder is a subdomain discovery tool that returns valid subdomains for websites, using passive online sources. It has a simple, modular architecture and is optimized for speed. subfinder is built for doing one thing only - passive subdomain enumeration, and it does that very well.

https://github.com/projectdiscovery/subfinder <br>
Here’s a simplified guide with common **Subfinder** commands:

 **Save Results to a File**  
   ```bash
   subfinder -d example.com -o subdomains.txt
   ```
 **Scan Multiple Domains**  
   ```bash
   subfinder -dL domains.txt -o output.txt
   ```

🔑 **Tip**: Add API keys in `~/.config/subfinder/config.yaml` for better results.

```
cat subdomain.txt | wc -l
```
For count howmany subdomains in subdomain.txt file

## httpx-toolkit
httpx probes URLs or IPs to determine their availability and fetch additional metadata. It supports a variety of protocols (HTTP/HTTPS) and methods to assess web servers efficiently.

The command:

```bash
cat domains.txt | httpx-toolkit > domains_final.txt
```

### **What It Does:**
1. Reads domains from `domains.txt`.
2. Pipes them to `httpx-toolkit` to check which are live.
3. Saves the live domains into `domains_final.txt`.

### **Purpose:**
- Filters live domains from a raw list.
- Output is saved in `domains_final.txt`.
---
Here is the updated command with `getadmiral_f.txt` changed to `domain.txt`:

```bash
httpx-toolkit -list domain_final.txt -silent -probe
```

### **Explanation:**

1. **`httpx-toolkit`**  
   - Executes the `httpx` tool to probe web servers.

2. **`-list domain.txt`**  
   - Specifies a file (`domain.txt`) containing a list of domains/URLs to process.

3. **`-silent`**  
   - Outputs only the live domains without extra details, making the output clean and concise.

4. **`-probe`**  
   - Ensures `httpx` probes both HTTP and HTTPS protocols for each domain to determine which services are available.

---

### **What It Does:**
- Checks the domains in `domain.txt` for live HTTP/HTTPS services.
- Outputs only the live results in a clean format.

### **Example Output:**
```plaintext
https://example.com [SUCCESS]
https://secure.example.net [FAILED]
http://test.example.com [SUCCESS]
```
---
for other knowlage see `httpx-toolkit -h` and https://github.com/projectdiscovery/httpx


## EyeWitness
https://github.com/RedSiege/EyeWitness

**EyeWitness** is a tool used to capture and display screenshots of websites. It helps security experts identify services and vulnerabilities on web servers. Here's a simplified explanation:

- **Purpose**: EyeWitness takes screenshots of websites (both HTTP and HTTPS) and collects useful information to help find potential issues on web servers.
- **Key Features**:
  1. Takes screenshots of websites.
  2. Collects HTTP response data (like headers).
  3. Identifies the technologies and services on the web server.
  4. Works with HTTP/HTTPS and can handle basic login prompts.
  
- **Use Case**: It's used in security testing to quickly view and understand multiple websites, helping to spot security risks.

---
The command:

```bash
eyewitness -f domains_final.txt --web --timeout 120
```

### **Explanation**:
- **`-f domains_final.txt`**: Uses the `domains_final.txt` file, which contains a list of domains to be processed.
- **`--web`**: Tells EyeWitness to capture screenshots of the websites.
- **`--timeout 120`**: Sets a 120-second timeout for each website to load.

### **What it does**:
It takes screenshots of the websites listed in `domains_final.txt`, with each site having a 120-second loading limit.