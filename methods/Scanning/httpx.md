
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
