
### For Finding Sub-Domains:
- **crt.sh**: Browser
- **Subfinder**: Kali
- **Oneforall**: Kali

### For Doing Fuzzing:
- **Ffuf**: Kali

### HTTPX-TOOLKIT:
Used for checking if a URL is working or not.

### For Doing Screen-shotting:
- **Eyewitness**: Kali

### To Find if a URL is Vulnerable or Not:
- **Subjack**: Kali

### Find JavaScript Files from URL:
- **Katana**: Kali
- **Subjs**: Kali
- **Getjs**: Kali

### Find JavaScript Files Secrets:
- **Secretfinder**: Kali
- Use the following key points:
  ```bash
  cat jsfile.txt | grep -r -E apikey | passwd | pwd | heroku | slack | firebase | swagger | aws key | password | ftppassword | jdbc | dbl sql | secret jet | config | admin | pwd | json | gcp | htaccess | .env | ssh key | .git | access key | secret token | oauth_token | oauth_token_secret
  ```
- **Mantra**: Kali

### GitHub Recon & Sensitive Data Exposure:
- **Gitdoker**: Tool
- **Manually Search in GitHub (BEST Method)**
- **Gitgraber**: Tool
- **Trufflehog**: Tool

### Finding Misconfigured AWS S3 Buckets:
- **Lazys3** 
- **s3Scanner**

### To Find Website ASN & CIDR:
- **ASN lookup**: Website
- **MX toolbox (CIDR range)**: Website
- **Asnmap (CIDR range)**: Tool
- **Mapcidr (CIDR to IP)**: Tool
- **DNSX (IP to Domain name)**: Tool

### Scanning Targets for Open Ports & Services:
- **mapCIDR**: Tool
- **nmap**: Tool
- **Naabu (port scanning tool)**: Tool
- **Masscan (Internet-scale port scanner)**: Tool
- **Rustscan**: Tool

## Find Low Hanging Fruits Vulnerabilities:

#### 1. Broken Link Hijacking:
Broken Link Hijacking exploits inactive or broken URLs to redirect users to malicious sites or gain unauthorized access.
- Tools:
  - **broken-link-checker**: Kali
  - Manual Testing
- Steps:
  1. Identify Broken Links: Use tools or manually test for URLs that return 404 errors.
  2. Verify Handling: Check how the site handles these links.
  3. Test Redirects: Observe if the site redirects to malicious locations.
  4. Analyze Responses: Ensure proper error pages are displayed.

#### 2. Missing SPF Record:
 A missing Sender Policy Framework (SPF) record can make a domain vulnerable to abuse, such as phishing, spam, and domain spoofing **(Most of case this vulnerability is out of scope. So first check this is in scope or not.)**
- Tools:
  - **Kitterman.com**: For checking
  - **Emkei.cz**: For sending fake mail
- SPF Record Examples:
  ```
  v=spf1 -mx -a 162.214.81.13 ~all
  v=spf1 -mx -a 162.214.81.13 -all
  v=spf1 -mx -a 162.214.81.13
  v=spf1 -mx -a 162.214.81.13 ?all
  ```

#### 3. Session Not Expiring After Logout:
Allows unauthorized access by failing to invalidate session tokens.
- Steps:
  1. Log in on multiple browsers.
  2. Change the password and test session validity on the other browser.
  3. Use session tokens to check access post-logout.

#### 4. Long Password DOS Attack:
Submitting excessively long passwords to overwhelm a system.
- Steps:
  1. Create an account and capture the request using Burp Suite.
  2. Modify the password to 500+ characters and send the request.

## Host Header Injection:
#### Vulnerabilities:
1. Open Redirection
2. Web Cache Poisoning Attack
3. Password Reset Poisoning Attack
4. XSS Attack

- Tools:
  - **Burp Suite**
- HTTP Status Codes: `2xx` or `3xx`
- Examples:
  ```
  Host: victim.com
  X-Forwarded-Host: hackersite.com

  Host: hackersite.com
  X-Forwarded-Host: victim.com

  Referer: hackersite.com
  ```
- Steps:
  1. Use a spider to explore a website.
  2. Modify the Host name or use `X-Forwarded-Host` or `Referer` headers.
### 2. Web Cache Poisoning Attack 
- When an attacker poisoned a cached version of information of a page and it get served to the equivalent requests then this is know as web cache Poisoning.

### 3.Password Reset Poisoning Attack

![Password Reset](img/Password%20Reset.png)

## HTML Injection:
HTML Injection is similar to XSS and can lead to:
- Phishing
- SSRF
- Impersonation
- Redirecting users to malicious websites

## LFI (Local File Inclusion):
Allows malicious users to access files on a web server.
#### Common Keywords:
- **File and Path Keywords**: `file=`, `path=`, `page=`, `include=`, `template=`, `dir=`, `action=, document=, folder=, load=, view=, content=, module=, url=, resource=, location=, site=, layout=,`
- **PHP File Inclusion Functions**: `include`, `require`, `include_once`, `require_once`

## Robots.txt:
The robots.txt file is a simple text file on a website that tells search engines which pages or sections they should not visit or index. It’s like a set of "do not enter" instructions for web crawlers, helping control which parts of the site appear in search results.

## SSRF: Server Side Request Forgery Vulnerability

**Server-Side Request Forgery (SSRF)** is a type of security vulnerability where an attacker tricks a server into making requests to unintended locations, such as internal systems or external malicious servers.

### Key Points:
- **What happens?**  
  The attacker sends a specially crafted request to the server.
  
- **What does the server do?**  
  The server, without checking if it's safe, makes the request on behalf of the attacker.
  
- **Why is it bad?**  
  The attacker can use the server to:
  - Access sensitive data.
  - Interact with internal systems that are not directly exposed.
  - Communicate with malicious external services.

## Example:
If a website fetches content from a URL provided by a user, an attacker might manipulate that feature to:
- Make the server access private systems.
- Leak sensitive information like database details or internal configurations.

---

Always validate and sanitize user inputs when handling URLs or external requests to prevent SSRF attacks.

### Bypassing Filters

```
Api_key = http://192.168.0.68/admin  // write sensitive-endpoint instead of admin
http://localhost/admin
http://127.1, etc 
```
`For more Bypassing Filters and knowlage`
https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/Server%20Side%20Request%20Forgery/README.md


## SQL Injection

### For more knowlage

https://github.com/kleiton0x00/Advanced-SQL-Injection-Cheatsheet?tab=readme-ov-file

### SQL 