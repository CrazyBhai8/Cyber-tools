# Wordpress Hunting

1. Admin Panel/ Dashboard 

2. Plugins- To increase the functionality of the website
3. Themes - Main website layout
Old Plugins- Vulnerable
Old Themes- Vulnerable

If website is on wordpress older version than previus versions have vulnerabilities.

#### Use: below dork for finding wordpress websites 
    https://github.com/Proviesec/google-dorks/blob/main/cms/google-dorks-for-wordpress.txt
    
    inurl:"wp-admin" (You can use also this type of commands)

### **Proper Workflow: Enumerating Users via the WordPress REST API**

1. **Find the Target URL**:  
   Identify the base URL of the WordPress site. For example:  
   ```
   https://www.example.com
   ```

2. **Append the REST API Endpoint**:  
   Add `/wp/v2/users` to the end of the URL to access the WordPress REST API for user information. The resulting URL will look like this:  
   ```
   https://www.example.com/wp/v2/users
   https://www.example.com/wp-json/wp/v2/users/12
   ```

3. **Make the Request**:  
   Use a tool like `curl`, a browser, or any HTTP client to make a GET request to the endpoint:  
   ```bash
   curl -X GET https://www.example.com/wp/v2/users
   ```

4. **Analyze the Response**:  
   - If the endpoint is accessible, it will return a JSON response containing the user information (e.g., usernames, user IDs, and potentially other public metadata).  
   - Example Response:
     ```json
     [
       {
         "id": 1,
         "name": "admin",
         "slug": "admin",
         "description": "",
         "url": ""
       },
       {
         "id": 2,
         "name": "editor",
         "slug": "editor",
         "description": "",
         "url": ""
       }
     ]
     ```

5. **Next Steps**:  
   Use the enumerated usernames (e.g., `admin`, `editor`) for further testing, such as password brute-forcing or privilege escalation.

---

### **Mitigation for WordPress Administrators**  
To secure your WordPress site against such enumeration:  
- Disable REST API access for unauthenticated users using security plugins (e.g., "Disable WP REST API").  
- Use strong, unique usernames and passwords.  
- Implement rate-limiting and CAPTCHA to prevent brute-force attacks.

---

## Finding Tools:
- wpscan: kali linux pre built tool.

### Enumeration Options (`-e`, `--enumerate`)

Use the `-e` flag with the following options to perform specific enumeration tasks:

| **Option** | **Description**                    | **Default Values**     |
|------------|------------------------------------|------------------------|
| `vp`       | Vulnerable plugins                |                        |
| `ap`       | All plugins                       |                        |
| `p`        | Popular plugins                   |                        |
| `vt`       | Vulnerable themes                 |                        |
| `at`       | All themes                        |                        |
| `t`        | Popular themes                    |                        |
| `tt`       | Timthumb files                    |                        |
| `cb`       | Config backups                    |                        |
| `dbe`      | Database exports                  |                        |
| `u`        | User ID range (e.g., `u1-5`)      | `1-10` if unspecified  |
| `m`        | Media ID range (e.g., `m1-15`)    | `1-100` if unspecified |

### Notes:
- Use commas (`,`) to combine options (e.g., `-e vp,vt,cb`).
- Default options: `vp,vt,tt,cb,dbe,u,m`.
- **Incompatible Groups:**  
  - Only one of these can be used at a time:
    - `vp`, `ap`, `p`  
    - `vt`, `at`, `t`.  
- For `m`, permalink settings must be set to **Plain**.

---
### commands:

```
wpscan --url "example.com" -e ap
```

**Note:** If you use the API key with WPScan, you can receive a detailed report of all vulnerabilities. It is highly useful for identifying potential security risks.

command
```
wpscan --url "example.com" --api-token 'TOKEN 3jenfakwn4309'
```

## For Exploiting

- CMSmap:- github tool
    - read all about it:- https://github.com/dionach/CMSmap
    ``` command
    cmsmap example.com
    ```
- Use & explore wpscan tool in kali to find vulnerable plugins or themes
- Use cmsmap to find different vulnerabilities & exploits in wordpress websites
## XML-RPC (Extensible Markup Language Remote Procedure Call.)
XML-RPC stands for Extensible Markup Language Remote Procedure Call. <br>
XML-RPC is a protocol used to send remote commands to servers via XML over HTTP. It’s often used in systems like WordPress for remote tasks like posting content or managing comments.

---

### **Types of Attacks on XML-RPC**  

1. **Brute Force Attacks:**  
   - Hackers guess login credentials using the `system.multicall` method to try many combinations at once.  
   **Fix:** Disable XML-RPC or limit login attempts.

2. **DDoS Attacks:**  
   - Overloads the server by sending too many requests using `system.multicall`.  
   **Fix:** Block or monitor XML-RPC traffic with a firewall.

3. **Data Injection (XSS/SQL):**  
   - Malicious data is sent through XML-RPC to exploit weak validation.  
   **Fix:** Validate all input and sanitize requests.

4. **Username Enumeration:**  
   - Attackers use XML-RPC to find valid usernames.  
   **Fix:** Restrict access or block the `wp.getUsersBlogs` method.

5. **Remote Code Execution (RCE):**  
   - Exploits vulnerabilities to run harmful code on the server.  
   **Fix:** Keep software updated and secure exposed methods.

---

### **How to Protect Against XML-RPC Attacks**  
- **Disable XML-RPC** if you don’t need it.  
- Use firewalls or security plugins to block bad requests.  
- Regularly update your software and monitor server activity.

---

### dorks and payload:
https://github.com/rm-onata/xmlrpc-attack

### Method 

### **Pingback.ping XML-RPC Payload**
```<?xml version="1.0" encoding="utf-8"?>
<methodCall>
  <methodName>pingback.ping</methodName>
  <params>
    <param>
      <value><string>https://www.postb.in/YOUR_BIN_URL</string></value>
    </param>
    <param>
      <value><string>https://www.TARGET.URL</string></value>
    </param>
  </params>
</methodCall>

```

### **Usage:**

You can also use https://webhook.site/ as an alternative to https://postb.in.
1. Replace `https://www.postb.in/YOUR_BIN_URL` with your Postb.in or Collaborator URL to capture requests.  
2. Replace `https://www.TARGET.URL` with the target URL you want to test.  

This payload sends a pingback request to the target, which is logged by the Postb.in URL for analysis.

---
## Summary
- Find all the subdomain of the target domain
- Find all the IPs related
- Hunt on those subdomain & IPs
- Try to find sensitive directories
- Try to find vulnerable plugins & themes
- Use CMSMap & WPSCAN tool along with NMAP

---
### msfconsole

commands 
```
msfconsole
search type: auxiliary wordpress xmlrpc
use MODULE_PATH
info  // (info use for all information about module)
show option
set RHOST website_name 
set RPORT 443 
```
---
### LAB
https://github.com/vavkamil/dvwp

we can use it as a lab.