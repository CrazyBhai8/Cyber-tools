# OSINT (Open Source Intelligence)

### Defination / Consept:

**OSINT** stands for Open Source Intelligence: it's a process of collecting and analyzing the publicly available information

## 1\. Introduction to Google Dorks

- **Google Dorks** are specialized search operators.
- They enable finding sensitive infromation not easily accessible through regular search.
- Useful for hacker, journalists and other individuals needing specific data.

## 2\. Searching for people

- **Target information:**  
    **Name:** Raju Don  
    **Schooling at:** LPU University

### 2.1 <ins>Double-quotes</ins>

This operator display result that exactly match your search query within double-quotes only

- Using it's we can reduce unnecessory result
- without double quotes result: 121,000
- with double quotes result: 3550 only

### 2.2 <ins>Inurl</ins>

Tells search engines to only look for specific keyword in URL.

`inurl:"raju don"`

- This shows only URL which have that specific keyword so these is helping in reduce result

### 2.3 <ins>OR</ins>

Searches for a given serch **OR** and equivalent term.  
`site:facebook.com OR site:twitter.com "raju don"`

- it means serch raju don keyword in facebook or twitter.com URLs
- OR must be written in capital letters

### 2.4 <ins>Intitle</ins>:

Display search result that contains a search term within the title of the page.

`intitle:raju.don`

==Note:== we can use dot(.) as space

### 2.5 <ins>Asterisk</ins>  \*:

Is a wildcard operator that acts as a placeholder for one or more words.

- Useful for finding middle names or filling in missing information in searches.

e.g. `"raju * don"` result → raju manu patel don

### 2.6 <ins>Hyphen</ins> (-):

Excludes a search terms from appearing in the search results.  
`"raju don" -site:linkedin.com`

- Here now remove all linkedin.com results

### 2.7 <ins>Site</ins>:

- Searches within a particular site
- Can be used to display search terms on that website.

e.g. `"raju don" site:instagram.com`

- now it's only shows instagram of raju don related results.

### 2.8 <ins>Filetype</ins>:

Tells search engines to only search for a specific file type.  
e.g. `site:"college.com" filetype:pdf`

- it's shows most of pdf files
- Download the PDF
- Go to this website [PDF metadata](https://www.metadata2go.com/)
- and extract all meta data.

In MetaData can find who create this pdf  
Author name, when, where, location etc.

* * *

## Other Search Engins

### Bing

Bing indexes different corners of the web than Google. It:

- Shows different cached pages
- Bypasses some search restrictions
- Indexes filetypes or uncommon sites better
- Sometimes finds leaks, logs, or exposed dirs missed by Google

### Bing Search Operators which not work on google

| Operator | What It Does | Example |
| --- | --- | --- |
| `ip:` | Finds pages hosted on a specific IP (Bing-only!) | `ip:198.51.100.34` |
| `contains:` | Finds pages with certain file types linked | `contains:xml site:gov` |
| `linkfromdomain:` | Pages linked **from** a specific domain | `linkfromdomain:example.com` |

### Yandex Search Engine

Yandex is Russia’s biggest search engine, indexing a different part of the web than Google or Bing.

- Yandex has some exclusive search operators that Google or Bing don't have.
- Using different search engines might yield varying search results.
- ==Yandex is the best for face matching and location identification==

### duckduckgo is also a good search engine

https://inteltechniques.com/tools/Search.html

- ==Using above tool easy to search in multiple search engines.==

* * *

## Google Hacking Database

**GHDB:** is an index of search queries that allow you to find sensitive/specific information on the internet.

- GHDB URL: https://www.exploit-db.com/google-hacking-database

Examples:

- Vulnerabilities
- Public cameras
- Public IOT devices
- Public Passwords
- Many more...

* * *

## Database Breaches & Leaks

## 1\. Introduction

### 1.1 Definition

- <span style="color: rgb(186, 55, 42);">**Data Leak**</span> is an unintentional exposure of sensitive data.
    
    - Human error
    - Overlooked vulnerabilities
- <span style="color: rgb(186, 55, 42);">**Data Breach**</span> is an intentional unauthorized access to sensitive information.
    
    - Exploited security vulnerability
    - **Data breach** is when someone gain unauthorized access of databse and extracts its data (like usernames, password, eamils, phone numbers, etc.)

### 1.2 Legality

- It's not allowed to use the data to access someone's else account.
- If data is public, possessing the data should be no problem.
- I am not a lawyer.

* * *

## 2\. Identifying Leaked Credentials

### 2.1 Required Information

At least one of the following

- E-Mail
- Phone Number
- Because it's always a unique Identity of the user.

Additional helpful information to **refine** your search:

- First and Last name
- Physical Address
- Country, City
- Age
- Gender

### 2.2 <ins>Have I been pwned? (HIBP)</ins>

HIBP - https://haveibeenpwned.com

**[HIBP](https://haveibeenpwned.com/)** allows you to check if your info are leacked onlied.

<ins>Utilizing HIBP in OSINT:</ins>

- Confirming email validity.
- Revealing individual interests.
- Shows what types of data were leaked.

### 2.3 <ins>DeHashed</ins>

DeHashed - https://dehashed.com/

**[DeHashed](https://dehashed.com/)** is a search engine to find data breaches and data leaks.

- This is a one of the best sevice for finding data breaches and leaks.
- But This is a paid service.🥲

### 2.4 <ins>IntelligenceX</ins>

IntelligenceX - https://intelx.io/

[IntelligenceX](https://intelx.io/) is a search engine and data archive.

- IntelligenceX is partially Free. and it's allow to search domain, URL, Email, IP, Bitcoin Address, and more.

How to use it.

1.  Go to: https://intelx.io
2.  Enter: target@email.com or site:example.com
3.  Choose the result type in Advanced : Paste, Leak, Darknet, etc.
4.  View raw dumps, archives, or related linked data.

| Feature | Free Plan | Paid Plan |
| --- | --- | --- |
| Search | Limited daily queries | Unlimited |
| Raw Dumps | Blurred or redacted | Full view |
| Export | Not available | CSV/JSON export |
| API Access | No  | Yes (powerful for automation) |

* * *

## Downloading Leak Breach Databases

### 1 Introduction - search in Leacked/Breached Databases

There are two ways to access data from a leaked or breached database:

1.  Subscription Service $$$
    - DeHashed, intelligenceX, Snusbase, etc.
2.  Local Download
    - Software: Agent Ransack and Torrent client
    - Hardware: Disk space

### 2\. Installing Needed Software to Manage Leaked Databases

### 2.1 Requirements

### 2.1.1 Create a Sock Puppet

Virtual Machine: Software emulation of a physical computer.

Features:

- Shares the resources of the host machine.
- Allow you to run multiple operating systems on one computer.

Why a VM is important for OSINT?

- Security
- Anonymity
- Isolation
- Operating System Flexibility

Installation of VM consider a youTure Video and install VM-ware Or Virtual Box & in OS install Kali.

### 2.2.2 Install uTorrent, and Mythicsoft in our Computer

Install Utorrent and Mythicsoft in our Computer

- uTorrent - https://www.utorrent.com/
- Mythicsoft - https://www.mythicsoft.com/

### 2.3 Downloading & Accessing Leaked Data

### 2.3.1 Facebook Leaked Database

Attackers exploited Facebook's contact importer feature in 2019.

- Over 500 million user profiles data were scraped.
- Data: User IDs, Phone numbers, and full names.

### **Finding :**

- Go to browser
- search facebook data leak github
- find github like https://github.com/davidfegyver/facebook-533m
- In this repo have magnet link. copy that.
- Go uTorrent
- Click on Add torrent
- Paste that magnet/torrent link there.
- Download it.

💥💥 BOOOOOOM 💥💥 - Now you have data.

- You can open the files in VS Code and search manually.
    
- Or, you can use the [Agent Ransack](https://www.mythicsoft.com/agentransack/download/) tool — it allows you to search across multiple files at once, helping you find specific data quickly. This saves time and avoids the need for manual, file-by-file searching.
    

### 2.3.2 Twitter Leaked Database

Attacked misued a Twitter API to match email addresses with Twitter Profiles.

- Over 200 million twitter profiles data were scraped.
    
- Compromised data: Email addresses, names. social media profiles, and usernames.
    
- ### **Finding :**
    
- Go to browser
    
- search twitter data leak github or like `"twitter 200m" "magnet:?"`
    
- it's means find twitter 200million data leak and it's should have magnet(uTorrent) link
    
- try to find magnet link. copy that.
    
- Go uTorrent
    
- Click on Add torrent
    
- Paste that magnet/torrent link there.
    
- Download it.
    

### 2.3.3 Linkedin Breached Database

- Occurred in 2012
- Publicly-available in 2017
- Databse contains 160+ million email addresses.

Compromised data: Member IDs, Emails, Passwords

Finding and Downloding methods as above.

- LinkedIn Data Breach (Without Passwords): https://archive.org/details/LIUsers.7z
- Finding Linkedin ID:
    - Go to that account
    - Go to page source
    - Do `Ctrl + F`
    - search `member:` keyword
    - You found Linkedin member ID which is unique of every linkedin person

### 2.3.4 Snapchat Breached Database

- Occurred in 2014
- Attackers misused Snapchat API to resolve usernames to phone numbers.
- Databse contains 6+ million records.

Compromised data: Phone numbers and usernames.

Finding and Downloding methods as above.

- SnapChat Data Breach : https://archive.org/details/SnapChat.7z

In this database, phone numbers are formatted like: 98989898XX — the last two digits are hidden with XX.

- To find the missing digits, go to the user's Facebook profile.
    
- Click "Forgot Password" — Facebook will show partially hidden phone numbers, including the last two digits.
    
- Match this with the known part (98989898XX) to reveal the full phone number.
    

### 2.3.5 Finding Leaked Databases on the Internet

<span style="color: rgb(186, 55, 42);">**Note:** When downloading leaked databases from the internet, you typically don’t know what’s inside. It is **highly recommended** to download and open such files **inside a virtual machine** or on a **dedicated, isolated machine** using a **separate network**. This reduces the risk of malware infections, spyware, or unwanted beaconing to external servers.</span>

### **Searching for Leaked Databases Online**

You can use advanced search queries to find leaked databases like:

```bash
"websitename.com.7z" "leak" "download" "magnet:?"
```

This dork searches for:

- Leaked database archives
- Magnet/torrent download links
- Files typically named after domain names

### **Other Resources for Finding Leak Databases**

- **Sizeof.cat**  
    📌 URL: https://sizeof.cat/post/data-leaks/  
    This site regularly posts **multiple leaked databases** and links to **searchable data dumps**.

* * *

## Building a Sock Puppet Identity for OSINT

### 1\. Creating an Untraceable Covert Account

### 1.1 Sock Puppet Accounts

Sock Puppet is a covert account that is not related to your identity.

This will prevent you from revealing your identity when performing SOCMINT.

### 1.1.2 Create a sock puppet

Virtual Machine: Software emulation of a physical computer.

Features:

- Shares the resources of the host machine.
- Allow you to run multiple operating systems on one computer.

**Set up your VM**  
**Why to use a sock puppet account in a VM?**

- Hide your real OS footprints from websites.(e.g. OS name, timeline, cookei etc)
- Protect your main system from malware.
- Quickly wipe your VM after an investigation is done.

### 1.1.3 Digital Identity / Covert Account

A **digital identity** or **covert account** is an **online persona** created to conceal your real identity during OSINT investigations, red teaming, or social engineering.

#### Key Traits:

- **Unconnected to your personal identity** (no real links to your name, email, or phone).
- Ideally, it should **mirror the target's environment**, language, and behavior to blend in.

## **Creating a Fake Identity**

Use the following tools to generate realistic personas:

### **Fake Name Generator**

- https://www.fakenamegenerator.com/
    
- Generates:
    
    - Full name
    - Address
    - Email
    - Phone number
    - SSN (for US profiles)
    - Credit card info
- Useful for creating detailed and believable online profiles.
    

### **AI-Generated Profile Pictures**

- https://thispersondoesnotexist.com/
- https://thispersonnotexist.org/
- These tools generate **AI-generated human faces** that do **not exist in real life**.
- Use them as profile pictures for fake social media or forums.

## ⚠️ Harpy’s Tip:

> Never reuse real images or identities. Always **compartmentalize your covert accounts**, use **virtual machines** or **isolated browsers**, and connect through **VPN or Tor** for maximum OPSEC.

* * *

## 2\. How to Keep Your Covert Account Safe & Active

Creating a covert identity is only the beginning. To avoid detection and keep the persona believable, you must maintain **operational security (OPSEC)** and **behavioral consistency**.

### **Checklist to Keep It Safe & Alive**

1.  Use a **virtual machine** or **dedicated browser** (isolated from your real identity).
2.  Create a **complete fake identity** using fake name generators.
3.  Set up a **Fastmail** email account.
4.  Get a **burner phone number** (temporary SIM).
5.  Connect through **public Wi-Fi** (like in libraries or cafes).
6.  Create **social media accounts** (Facebook, Instagram, X, etc.).
7.  Keep the accounts **active** (post content, follow users, comment).
8.  **Log in at least twice a week** to avoid account flagging or removal.

### **Create a Fastmail Email**

- Visit: https://www.fastmail.com/
- Sign up with your puppet identity details (name, fake DOB, etc.)
- Use “Try for Free” to test the setup.

> ⚠️ Fastmail may ask for **phone number verification**. Skip this for now — see next step.

### **Get a Burner Number**

#### If you're in the **USA**:

- Buy a temporary SIM card like:  
    [Mint Mobile Prepaid SIM - BestBuy](https://www.bestbuy.com/site/mint-mobile-prepaid-sim-card-starter-kit-gold/6310601.p)

#### If you're in a **European country**:

- Use: https://www.lebara.nl/en/home.html  
    (Lebara offers cheap, prepaid SIM cards usable for verification)

> Burner numbers are essential for verifying accounts like Facebook or email without using your real phone.

### **Use a Library or Café Wi-Fi**

> Public Wi-Fi is better than VPN in some cases because:

- Sites like Facebook can detect and flag **VPN or proxy connections** as suspicious.
- Library or café Wi-Fi helps maintain a **natural login pattern**.

### **Keep the Account Active**

- Add a few friends or follow relevant accounts (based on your persona).
- Post believable content (quotes, selfies from AI-generated images, memes).
- Like, share, and comment occasionally.
- Avoid doing **nothing** — that’s a red flag for algorithms.

### **Login Frequency & Security**

- **Log in at least twice a week** to keep the account in good standing.
    
- Set up **2-Factor Authentication (2FA)** using:
    
    - Authenticator app (not linked to your real number)
    - Burner phone for SMS-based 2FA (only if needed)

* * *

## Social Media Intelligence (SOCMINT)

### Introduction to SOCMINT

**What is SOCMINT?**  
Social Media Intelligence (SOCMINT) is a subdomain of OSINT focused on collecting, analyzing, and exploiting data from social media platforms like Facebook, Instagram, Twitter (X), LinkedIn, TikTok, and others.

> It involves monitoring public posts, user profiles, connections, behaviors, and hidden metadata to gather actionable intelligence.

## <span style="color: rgb(37, 92, 217);">1\. Facebook OSINT</span>

* * *

### 1.1 Intro

People post all kinds of information on social media.

- Facebook has more then 3 billion active users.

<span style="color: rgb(37, 92, 217);">Facebook</span> is a good source to gather information:

- Vast user base
- Profile Information
- Connections and Relationships
- Diverse Content
- Geotagged Content
- Publicly Accessible Content

### 1.2 Extracting User ID, Facebook Friends & More

**User ID:** Every Facebook user has a unique identifier that's gets generated once a Facebook profile is created.

- Example: 100003303000000

### **Find Facebook User ID**

### Steps to Get the User ID:

1.  Go to the **target's Facebook profile**.
2.  Right-click and select **"View Page Source"** or press `Ctrl + U`.
3.  Use `Ctrl + F` and search for:

```
"userID"
```

4.  You’ll find a line like:

```json
"userID":"100003303000000"
```

### **Find ID via Website Tool**

- Use: https://findidfb.com/
- Just paste the user’s Facebook profile URL.
- The site will **automatically fetch and display the Facebook User ID**.

This is their **unique Facebook ID**, which **never changes**, even if they:

- Change their **display name**
- Change their **username**
- Set their profile to private

### **How to Use Facebook User ID**

If the target changes their custom username or display name, you can still access their profile like this:

```url
https://www.facebook.com/100003303000000/
```

> This works **regardless of name changes**, as the numeric ID is **permanent** and tied to the account itself.

### Example:

- Suppose the user’s custom URL was:

```url
https://www.facebook.com/username/
```

But they change it or delete the username…

You can still visit their profile directly using:

```url
https://www.facebook.com/100003303000000/
```

### Account creation date.

![ebb8b34a3fb75e1e003c04f02894915a.png](../_resources/ebb8b34a3fb75e1e003c04f02894915a.png)

### Find ID by website

Find Facebook ID: https://findidfb.com/

- Just paste you URL. this website automatically featch your userID.

### **1.3 Save Facebook Friend List (Manual Method)**

Facebook can detect automated tools and extensions that save friend lists — using them can **trigger account flags or blocks**.

### Browser Extensions:

There are Chrome/Firefox extensions that claim to save friend lists, but **Facebook’s detection systems** can flag such activity.

> ❌ Not recommended for covert or long-term accounts.

### **Manual Safe Method:**

1.  Go to the **user’s friend list page**.
2.  **Scroll to the bottom** to ensure all friends are fully loaded.
3.  **Select all visible friends** (`Ctrl + A`)
4.  **Copy** (`Ctrl + C`)
5.  Paste into **Excel** or **Google Sheets** (`Ctrl + V`)
6.  Clean up and organize as needed.

This method is:

- **Safe** (no automation = low risk)
- **Stealthy** (Facebook won’t detect it)
- **Quick** if you just need basic friend names

### **1.4 Uncovering Emails and More from Facebook Profiles**

Utilize the "Forgot password?" feature on Facebook to find contact information associated with a Facebook account.

### Steps to Use "Forgot Password?" for OSINT:

### Step 1: Go to Facebook Login Page

- Visit: https://facebook.com
- Click on: **“Forgotten password?”**

### Step 2: Enter the Target’s Info

- In the input box, enter **one of the following**:
    
    - Facebook **username**
    - Custom profile **URL**
    - **Real name** (if unique)
    - Or better: the **User ID** (like `https://facebook.com/1000xxxxxxxxxx/`)

### Step 3: Facebook Will Search for the Account

- It will display the **profile picture** and **name** to confirm identity.
    
- Then it will show options like:
    
    - **Email (partially hidden):**  
        `••••••@g•••.com`
    - **Phone number (partially hidden):**  
        `+91 98•• ••874`

These **partially revealed details** can help you:

| Info You Know | What You Can Confirm |
| --- | --- |
| First part of email | Is it a Gmail, Yahoo, etc. |
| Last digits of phone | Match to leaked database formats |
| Phone prefix | Helps identify country, region, or carrier |

### Step 4: Pivot the Data

Once you have:

- Last 2–4 digits of the phone number → Compare with known formats
- Email structure → Reverse search on **HaveIBeenPwned**, **Dehashed**, or **Hunter.io**

### 2.5 Finding CommentsTags of a Facebook Account

Utilizing search engine operators can be useful in locating publicly indexed comments and tags.

```bash
"name" site:facebook.com inurl:posts
```

Helps find:

- Comments
- Public tags
- Group interactions
- Public status updates

Use additional dorks to expand results.

### Summary

- Use **filters** to locate the target profile.
- Save the profile picture.
- Check the username.
- Find the User ID.
- Identify the account **creation date**
- **Review** all posts.
- Save the public friend list.
- Try the **forgot password** feature on FB.
- Search for public info using **search operators**

## <span style="color: rgb(252, 176, 69);">2\. Instagram OSINT</span>

* * *

### 2.1 Intro of Instagram

<span style="color: rgb(252, 176, 69);">Instagram</span> has over 1 billion monthlyactive users.

- Users can only share photos and videos.

### 2.2 Find a User ID of a Instra Profile

**User ID:** Every Instragram user has a unique identifier that's gets generated once an Instragram profile is created.

- Example: 49279209744
- Press, `Ctrl+u` to view the page source
- Search for `profile_id`

**Find ID by Username**

- Find Instagram ID by fameswap.com: https://fameswap.com/tool-instagram-user-id
    
- Find any Instagram User ID by Instagram username: https://commentpicker.com/instagram-user-id.php
    
- Just paste you URL. this website automatically featch your userID.
    

**Find Username by ID**  
If your victim change his username and you can't find him/her. But you have it's User ID. then,

- Get any Instagram username from an Instagram user ID: https://commentpicker.com/instagram-username.php

### 2.3 Extracting Timestamps from Posts and Comments

**TImestamp:** will show you the exact data and time when a post was posted.

- Format: yyyy-MM-dd'T'HH:mm:ss

```html
::before
<time class="x1p4m5qa" datetime="2025-04-19T16:52:04.000Z" title="19 April 2025">19 April</time
::after
```

**Steps to Extract the Timestamp:**

1.  Go to the **target Instagram post or comment**.
2.  Right-click the **post time/date** (e.g. *“8w”*, *“19 April”*).
3.  Click **"Inspect"** (or press `Ctrl + Shift + I`).
4.  In the source code, locate the `<time>` tag.
5.  Copy the `datetime` value:  
      `2025-04-19T16:52:04.000Z`
6.  Go to: [timestamp-converter.com](https://www.timestamp-converter.com/)
7.  Paste the timestamp into the converter.
8.  You will see the **exact local time** in your time zone.

### 2.4 Uncovering Comments of Private Instagram Accounts

Utilize search engine operators to discover indexed information on instagram profiles.

```url
site:instagram.com "Username"
site:instagram.com "@Username"
site:twitter.com "username" "instagram.com/p"
```

- You can direct paste Profile URL:  
    `https://www.instagram.com/username/` on google, bing, yandex search bar and got result like where user liked, comment, posts etc.

### 2.5 Extracting Hidden Information from Instagram Metadata

### **What is Instagram Metadata?**

**Account Metadata**

- **Metadata** can something contain useful information
- **Browser Extention:** User-Agent Switcher and Manager

**Metadata** refers to hidden or background information embedded within content or served through APIs — such as device type, operating system, full-size profile pictures, and sometimes extra details not shown on the main app or website.

Instagram’s web interface **hides some data** unless it thinks you’re using a mobile device.  
We can bypass this by **changing the browser’s user agent** to mimic an Android device.

### **Tools You Need**

To do this, use a browser extension like:

- 🔹 [User-Agent Switcher and Manager – Chrome](https://chromewebstore.google.com/detail/user-agent-switcher-and-m/bhchdcejhohfmigjafbampogmaanbfkg)
- 🔹 [User-Agent Switcher and Manager – Firefox](https://webextension.org/listing/useragent-switcher.html?version=0.6.4&type=install)

### **How to Use (Step-by-Step)**

1.  Go to the target's **Instagram profile**.
    
2.  Open the **User-Agent Switcher and Manager** extension.
    
3.  Select:
    
    - **Device**: Android
    - **Site**: Instagram
    - **User Agent**: Choose any Android browser
4.  Click **Apply (All Tabs)** — this sets your browser to act like a mobile device.
    

### **Accessing Metadata**

Now you’re ready to pull hidden details using Instagram’s mobile endpoint.

#### Use this URL format:

```url
https://i.instagram.com/api/v1/users/USER_ID/info/
```

- Replace `USER_ID` with the **actual user ID** of your target. (e.g. 49279209744)
- Example:  
    `https://instagram.com/49279209744/`

Open the link in your browser **with the mobile user agent active**.

### **Why This Is Useful**

- Normally, when you try to download someone’s **Instagram profile picture**, it gives you a **low-res 320×320** version.
- But when accessing the profile with a **mobile user agent**, Instagram serves the **HD version** of the profile picture — often up to **1080×1080 or higher**.

You can **right-click → Open image in new tab → Save HD profile picture**.

### 2.6 Scraping Instagram Followers

### Download Information

**Manual Method:**

- Required effort
- Time-consuming
- Generally reliable

**Automatic Method:**

- Fast data collection
- Requires minimal effort
- Tools may not work in the future
- Risk of account suspension or banning

### Download all followers

1.  Go to the **user’s followers list page**.
2.  **Scroll to the bottom** to ensure all followers are fully loaded.
3.  **Select all visible friends** (`Ctrl + A`)
4.  **Copy** (`Ctrl + C`)
5.  Paste into **Excel** or **Google Sheets** (`Ctrl + V`)
6.  Clean up and organize as needed.

If profile pictures are also copy and paste in Excel then,  
**Remove that profile pics**

1.  Press F5
2.  Click on **special**
3.  Select objects
4.  click OK
5.  Press Delete key on keyboard

## **Filtering URL and Display Name in Excel**

1.  **Select the column** where your data is stored (e.g., Column A).
    
2.  Go to the **`Data`** tab in the top menu.
    
3.  Click on **`Filter`**.
    
4.  A small **dropdown arrow (▼)** will now appear next to the column name (e.g., A1).
    
5.  Click on the dropdown arrow.
    
6.  Choose:
    
    - **"Filter by Color"** – if you’ve highlighted rows.
    - **"Text Filters"** – to filter by keywords like "facebook.com", "gmail", or names.

## **Get Instagram Followers Data Using Extension**

Instead of manually scrolling and copying follower lists, use a browser extension to **extract and export Instagram follower data** efficiently.

> ⚠️ **Important:**  
> Always use a **puppet (fake) account** when using automation tools. Instagram may detect this activity and **ban or restrict your account**.

### **Extension Used**

🔗 [**IG Follower Export Tool - IG Tools** (Chrome)](https://chromewebstore.google.com/detail/ig-follower-export-tool-i/kicgclkbiilobmccmmidfghnijgfamdb)

### **Steps to Use the Extension**

1.  Log in to **Instagram** using your **puppet account**.
2.  Go to the **target user’s profile**.
3.  Click the **IG Follower Export Tool** extension icon in your browser.
4.  Click **“Export Instagram Data”**.
5.  In the input field, enter the **Instagram handle** or full profile URL:  
    Example: `@username` or `https://www.instagram.com/username`
6.  Increase the **delay time** (e.g., `10s`) to avoid detection or temporary blocks.
7.  Click **“Start New Parsing”** to begin scraping the follower list.
8.  After the process completes, click **“Save to Excel”** to download the data.

**Output includes:** ID, username, name, profile URL, avatar, verification, follow status  
Absolutely, Falcon 🦅 — here's your cleaned-up, properly formatted, and **OSINT-friendly** version of:

## 2.7 Downloading Instagram Posts

Whether you're archiving a target's content for OSINT, digital profiling, or offline analysis, there are **two ways** to download Instagram images: manually or using browser extensions.

### **Manual Method (One Post at a Time)**

Use this when you only need to download **a few images**:

1.  Go to the **Instagram post**.
2.  Right-click on the page and click **Inspect** (or press `Ctrl + Shift + I`).
3.  Locate and **select the image element** (inside the HTML code).
4.  Copy the **image URL** from the `src` attribute.
5.  Paste the URL in a **new browser tab**.
6.  Right-click and **save the image**.

> ⚠️ This method is time-consuming if the user has **many posts**.

### **Browser Extension Method (Bulk Download)**

If the account has **dozens or hundreds of posts**, use a tool like:

🔗 [**Download All Images – Chrome Extension**](https://chromewebstore.google.com/detail/download-all-images/nnffbdeachhbpfapjklmpnmjcgamcdmm?hl=en)

### **Steps to Use the Extension:**

1.  Go to the **target’s Instagram profile**.
    
2.  **Scroll down** until **all the posts are loaded** (important!).
    
3.  Click the **Download All Images** extension in your browser.
    
4.  In the extension settings:
    
    - Select image type (e.g., `JPG`)
5.  Wait for the extension to finish scanning the page.
    
6.  Click **Save** — all images will be downloaded as a **ZIP file**.
    

### Notes:

- This works **only for public profiles**.
- For private accounts, you must be **following the target** with a valid or puppet account.
- Instagram might **rate-limit or throttle** image loads if you're scraping too fast — keep it human-like.

### 2.8 Download Instagram Content by linux tool

### Set up OSINT VM

**TraceLabs VM** is a customized version of kali Linux focused solely on OSINT tools.

**Why to use a Linux distribution?**

- Pre-configured Enviroment
- Tool Compatibility

### Download Instagram Content

**Instaloader** is a tool to download picture/video along with their captions and metadata from an Instagram account.

- Install: `pip install instaloader`
- Go to documentation of [InstaLoader](https://instaloader.github.io/)

it's a kali tool which help you to download posts,videos, followers, following etc.

## <span style="color: rgb(36, 158, 240);">3\. Twitter / X OSINT</span>

* * *

### 3.1 Introduction

X has over ca. 550 mil. monthly active users.

- Users can tweet, share photos, video and add links.

### 3.2 Recovering Deleted Tweets and Timestamps

**Find a User ID of Twitter / X Profile**

**User ID:** Every Twitter / X user has a unique identifier that's gets generated once an Instragram profile is created.

- Example: 1430275132268883203
- Press, `Ctrl + Shift + i` to run inspect elements
- Search for `/profile_banners/` OR `identifier`

**Find ID by website**  
Find Twitter / X ID: https://commentpicker.com/twitter-id.php

- Just paste Url OR Username. this website automatically featch your userID.

**Extracting Timestamps from Posts and Comments**

**TImestamp:** will show you the exact data and time when a post was posted.

- Format: yyyy-MM-dd'T'HH:mm:ss

**Steps to Extract the Timestamp:**

1.  Go to the **target Twitter post or comment**.
2.  Right-click the **post time/date** (e.g. *“8w”*, *“19 April”*).
3.  Click **"Inspect"** (or press `Ctrl + Shift + I`).
4.  In the source code, locate the `<time>` tag.
5.  Copy the `datetime` value:  
      `2025-04-19T16:52:04.000Z`
6.  Go to: [timestamp-converter.com](https://www.timestamp-converter.com/)
7.  Paste the timestamp into the converter.
8.  You will see the **exact local time** in your time zone.

### Indexed tweets

Utilize search engine operators to discover indexed information on instagram profiles.

```url
site:twitter.com "Username"
site:twitter.com "@Username"
site:twitter.com/Username/status
```

### 3.3 Leveraging Search Operators to Find Specific Tweets

**Twitter/X advanced search operators** allow you to **refine**, **filter**, and **extract** tweets based on specific users, dates, and interactions — extremely useful for SOCMINT and digital recon.

### Common Twitter Search Operators

- `from:username` → Shows all tweets **made by** that user
- `to:username` → Shows all tweets **sent to** that user
- `since:YYYY-MM-DD` → Filters tweets **starting from** a date
- `until:YYYY-MM-DD` → Filters tweets **up to** a date (exclusive)

**Example Search Query**

```bash
from:username since:2024-01-01 until:2024-01-15
```

This will return:

> All tweets **from the user** posted between **January 1, 2024** and **January 14, 2024** (Note: `until` is *exclusive* of the date itself).

### Summary

- Analyze and save the username, bio, and profile picture.
- Get the User ID
- Posts/Commets Timestamp
- Find any indexed Tweets
- Use Twitter Operators

## <span style="color: rgb(18, 107, 196);">4\. Linkedin / X OSINT</span>

* * *

### 4.1 Introduction

<span style="color: rgb(18, 107, 196);">**Linkedin**</span> has over ca. 900 mil. users.

- Users can post, share photos, video and add links.

### 4.2 Discovering and Analysing LinkedIn Profiles

**Search Filters**  
Linkedin **Filters** help:

- Narrow down search results
- Save time and effort

**Profile Overview**

- Analying the target profile

**Download Information**  
Linedin makes it very easy for us to download someone's profile.

- Go to target profile
- Click on `more`
- Click on `Save to PDF`  
    You can download profile as resume

### **4.3 Finding Hidden Names & Extracting Post Timestamps**

This section covers two powerful LinkedIn OSINT techniques:

- Extracting **exact timestamps** from posts and comments
- Uncovering **redacted/hidden employee names** on company pages

### **Extracting Post Timestamps**

LinkedIn **encodes timestamps** in post and comment URLs. Here's how to decode them:

#### For Posts

1.  Copy the **Post URL**  
    Example:
    
    ```
    https://www.linkedin.com/feed/update/urn:li:activity:732589268174922370/
    ```
    
2.  Extract the **Post ID**:
    
    ```
    732589268174922370
    ```
    
3.  Convert the Post ID to **binary**  
    Use: [RapidTables Decimal to Binary](https://www.rapidtables.com/convert/number/decimal-to-binary.html)  
    Example Output:
    
    ```
    1010001001010101001000111110110010101101000001010000010
    ```
    
4.  Take the **first 42 bits** of the binary value.
    
5.  Convert those 42 bits back to **decimal**  
    Use: [Dan's Timestamp Tool](https://www.unixtimestamp.com/)  
    Paste the decimal into the timestamp field.
    

his will reveal the **exact time the post was created** (in UTC or local).

#### For Comments

1.  Find the **three-dot menu** next to the comment.
2.  Click **"Copy link to comment"**.
3.  Extract the **comment ID** from the URL.
4.  Repeat the **binary + timestamp** process above.

### Alternative Tool: **Unfurl**

For fast results:

- Use [Unfurl Tool](https://dfir.blog/unfurl/)
- Paste the **LinkedIn post or comment URL**
- The tool will automatically extract the **timestamp and other metadata**

## **Finding Redacted Names (Hidden LinkedIn Employees)**

LinkedIn sometimes **censors employee names** on company profile pages — especially when you’re not logged in or if your account isn’t trusted.

> Example: You visit a company’s “People” section and some entries just say "LinkedIn Member".

### How to Reveal Hidden Names

Use Google Dorks to bypass LinkedIn's frontend filters.

#### 🔍 Dork:

```bash
site:linkedin.com/in/ "job description" "company name"
```

- Replace `"company name"` with the actual target company
- Replace `"job description"` with a likely title (e.g. `"security analyst"`, `"marketing manager"`)

This pulls profiles indexed by Google — including names that are **redacted in-app**.

### Summary

- Use Filters to narrow your search
- Analyze the target profile
- Posts/Comments Timestamp
- Find redacted names.

### 4.4 Finding LinkedIn Profile Member IDs

### **Steps to Find a LinkedIn Member ID:**

1.  Go to the **target’s LinkedIn profile** page.
    
2.  Right-click → Click **“View Page Source”** or press `Ctrl + U`.
    
3.  Press `Ctrl + F` to open the **search bar**.
    
4.  Search for:
    
    ```
    member:
    ```
    
5.  You’ll find a line like this:
    
    ```json
    "member:123456789"
    ```
    
    - The number (`123456789`) is the **LinkedIn Member ID**.
    - It’s unique to each LinkedIn user.

### ⚠️ Important Tip

> **Always double-check** the ID you find.  
> If you're logged into your own account, you might accidentally extract **your own member ID** instead of the target’s.

## 5\. Other Social Media OSINT

### <span style="color: rgb(255, 251, 9);">**5.1 Snapchat OSINT**</span>

* * *

### **Downloading Public Snapchat Stories**

You can use public tools to view and download **Snapchat stories** posted by a user.

#### Tool:

🔗 [Snapchat Story Viewer & Downloader](https://snap.storyclone.com/)

#### Steps:

1.  Go to: https://snap.storyclone.com/
2.  Paste the **Snapchat profile URL** or **username**.
3.  The tool will display all **publicly available stories**.
4.  Download any video or image — stories often come with **timestamps**.

> **Note:** Timestamps are shown in **UTC**.  
> Use tools like [savvytime.com](https://savvytime.com/converter) to convert them to your victim’s **local timezone**.

### **Getting Snapchat Avatar (Snapcode)**

You can fetch the user’s **Snapcode avatar** in high-quality SVG format.

#### Use this URL:

```url
https://app.snapchat.com/web/deeplink/snapcode?username=USERNAME&type=SVG
```

- Replace `USERNAME` with the **Snapchat handle** of your target.
- This will return their **Snapcode avatar** (scannable QR-like code) in vector format.

Example:

```url
https://app.snapchat.com/web/deeplink/snapcode?username=johndoe&type=SVG
```

## <span style="color: rgb(115, 5, 124);">**5.2 TikTok OSINT**</span>

* * *

**TikTok** has over **1.3 billion users**, making it a goldmine for digital investigators. TikTok profiles, videos, and metadata often expose valuable insights that can be collected and analyzed using OSINT techniques.

## **Profile Overview**

When viewing a target profile, pay attention to:

- **Username** vs. **Display name** (they can differ)
- **Bio links** (may lead to other platforms)
- **Profile Picture** (can be saved & reverse searched)

## **Extracting Timestamps**

### For TikTok Posts

TikTok video URLs often contain a unique **video ID** that embeds a timestamp.

#### Steps:

1.  Copy the **TikTok post URL**  
    Example:
    
    ```
    https://www.tiktok.com/@username/video/7234567890123456789
    ```
    
2.  Extract the **Video ID**:
    
    ```
    7234567890123456789
    ```
    
3.  Convert the ID to **binary** using:  
    [RapidTables Decimal to Binary](https://www.rapidtables.com/convert/number/decimal-to-binary.html)
    
4.  Take the **first 32 bits** of the binary output.
    
5.  Convert those 32 bits back to **decimal**.
    
6.  Paste the decimal into a **Unix timestamp converter**
    
    - Use: https://www.timestamp-converter.com/
    - Or: https://dfir.blog/unfurl/ (paste full URL)

You now have the **exact post time (in UTC)**.

### For TikTok Comments

1.  Right-click on the **comment timestamp** → Click **Inspect**.
2.  Locate the **comment ID** in the HTML.
3.  Use [Unfurl](https://dfir.blog/unfurl/) — paste the **comment ID only**.
4.  It will extract and display the **timestamp**.

## **Download TikTok Videos (No Watermark)**

🔗 Use: https://freetik.co/

#### Steps:

1.  Copy the TikTok video URL.
2.  Go to [freetik.co](https://freetik.co/)
3.  Paste the URL and click **Download**.
4.  Choose from available formats (HD, no watermark, etc.).

## **Extract Hidden Metadata**

TikTok embeds hidden JSON data inside the profile page.

#### Steps:

1.  Go to the **target’s TikTok profile**.
    
2.  Right-click → Click **Inspect**.
    
3.  Scroll down the HTML until you find:
    
    ```html
    <script id="__UNIVERSAL_DATA_FOR_REHYDRATION__" type="application/json">
    ```
    
4.  Inside this tag is a full **JSON block** with metadata (followers, likes, videos, etc.)
    
5.  **Copy the JSON**, paste it into **Notepad**, and save as:
    
    ```
    target.json
    ```
    

You can later open and analyze it in tools like:

- VS Code
- JSONView browser extension
- JQ (command line)

### Summary

- Analyze the target profile
- Postes/Comments Timestamp
- Download Videos
- Extract Metadta

* * *

## Other OSINT Techniques.

1.  Username OSINT
    - Tracking Online Identities
2.  People OSINT
    - Uncovering Personal Information Online
3.  Email OSINT
    - Finding Email Addresses
    - Discovering Info Linked to an Email Address
4.  Phone Number OSINT
    - Discovering Phone Numbers
    - Finding Details Behind a Number
5.  Image OSINT
    - Reverse Image Search
    - Facial Recognition
    - Geo Location Tracking
6.  Maps OSINT
    - Using Maps for Geolocation Analysis
7.  Websiter OSINT
    - Analyzing Website Data for Intelligence
    - OSINT TraceLabs VM

## 1\. Username OSINT

### 1.1 Tracking a Username Using Advanced Search Techniques

**Step 1: Gather Online Usernames**  
After collecting info on your target, save all found usernames in a text file for future searches.  
Example:

```
user-name
_Username420
un132
user-name_
```

**Step 2: Search Operators**  
Use search operators to see if a username is indexed by search engines.

**Format:**

```plaintext
inurl:username1 OR inurl:username2 OR inurl:username3
```

**Purpose**: Helps you uncover accounts on other platforms like Quora, Cloudflare, Pinterest, Medium, etc.

## **1.2 Finding Hidden Profiles with Reverse Username Lookup**

### **People Search Engines**

One powerful tool for reverse username lookups is **ID Crawl**.

**Website:** https://www.idcrawl.com/

**How to Use ID Crawl:**

1.  Go to [ID Crawl](https://www.idcrawl.com/).
2.  Enter the **username, email, phone number, or full name**.
3.  Review the results — this may include **social media profiles, blogs, and forum accounts**.
4.  Note all linked accounts and verify them using other OSINT tools.

*Pro Tip:* Try multiple variations of the username — add/remove numbers, change underscores, try different capitalizations.

## **1.2 Finding Hidden Profiles with Reverse Username Lookup**

### **People Search Engines (Websites)**

These are online tools you can use directly in your browser:

- **ID Crawl** → https://www.idcrawl.com/
    
    - Finds **social media profiles, blogs, and mentions** linked to a username, email, phone number, or full name.
    - Good for quick, non-technical searches.
- **WhatsMyName (Web version)** → https://whatsmyname.app/
    
    - Searches **500+ websites** for accounts linked to a username.
    - Gives direct links to possible profiles.

### **Command-Line & GitHub OSINT Tools**

For deeper and automated searches across more platforms:  
<span style="color: rgb(186, 55, 42);">**Note:** <span style="color: rgb(224, 62, 45);">Some result are may be false positive. so always check all results</span></span>

- **WhatsMyName (CLI version)** → https://github.com/WebBreacher/WhatsMyName
    
    - Run locally with Python for faster and bulk username checks.
- **Blackbird** → https://github.com/p1ngul1n0/blackbird
    
    - Scans usernames across social media, forums, and gaming platforms.
    - CLI tool for **faster and customizable searches**.
- **Sherlock** → https://github.com/sherlock-project/sherlock
    

**Sherlock** is a tool to search for a given username on hundreds of websites.

- Some result are false positive.
    - Searches **300+ platforms** for accounts.
        
    - Example:
        
        ```bash
        python3 sherlock username123 username2 
        ```
        

- **Maigret** → https://github.com/soxoj/maigret
    
    - Checks **2,500+ websites** and exports results to **HTML, JSON, PDF**.
        
    - Example:
        
        ```bash
        maigret username123 -a -o results.html
        ```
        

### **1.3 Search in Leaked Databases**

Searching for a **username** (or related email/phone) in leaked/breached databases can reveal additional information such as:

- Associated **email addresses**
- **Phone numbers**
- **Passwords** (hashed or plaintext)
- Other linked accounts

### **Websites (Online Tools)**

- **DeHashed** → https://dehashed.com/
    
    - Search leaks by **username, email, IP, phone number, or password**.
    - Requires account (paid plan for full results).
- **LeakPeek** → https://leakpeek.com/
    
    - Simple interface, free limited searches.
    - Good for checking if a username/email appears in known breaches.
- **BreachDirectory** → https://breachdirectory.org/
    
    - Fast results, often shows partial passwords for free.
- Always **cross-check usernames with emails** from the same leak — you might uncover secondary accounts.

### Summary
- Collect the person's usernames.
- Search for usernames on search engins.
- Use people search engin / online tools to find additional accounts with the same username.
- Search in leaked databases.

## **2. People OSINT**

### **2.1 Finding the Geographic Origins of a Name**

**Name origin analysis** can help you **narrow down your search** by identifying possible countries, regions, or ethnic backgrounds where the name is common.


#### **Tools & Websites**

1. **FamilySearch – US Public Records**
   **Website:** [https://www.familysearch.org/en/united-states/](https://www.familysearch.org/en/united-states/)

   * Contains **U.S. public records** and genealogy data.
   * If your target is **not from the USA**, you may not find them directly.
   * However, under the **"Last Name Information"** tab, you can get clues about **geographic distribution** of a surname within the U.S. — this can suggest possible migration patterns.

2. **NamSor – Name Origin & Gender Analysis**
   **Website:** [http://namsor.app/](http://namsor.app/)

   * Uses **machine learning** to predict the **country of origin**, **ethnicity**, and **gender** from a given name.
   * Works with **first name, last name, or both**.
   * More accurate for **global names** compared to U.S.-only databases.
   * Can also detect if a name appears to be **Westernized** or altered.

3. **social-searcher**
	**Webste** [https://www.social-searcher.com/](https://www.social-searcher.com/)

After knowing country. you can search like:
`"username" "india"`

### 2.2 Find Personal Details Using Advanced Search Techniques 
Use search operators to check if a person's information is indexed by search engines.

**Format:**
```url
"first and last name" "city" OR "country" OR "University" OR "company"
```

<span style="color: rgb(186, 55, 42);">**Note:** Sections 2.3–2.6 focus mainly on U.S. citizen data sources. </span>

### 2.3 Discovering Phone Numbers, Addresses, DOB, and More 

People Search Engines are websites for finding info on individuals, mainly for US citizens.
**People Search Engines** are specialized websites for gathering personal information, mainly for **U.S. citizens**.
These platforms compile public records, online listings, and other data sources to help locate individuals.

**Information You Can Find:**

* Full name(s) and aliases
* Current and past phone numbers
* Physical addresses (current & previous)
* Date of birth (DOB)
* Relatives and associates
* Email addresses (sometimes)

#### **Important Notes:**

* Many of these websites **restrict access to U.S. IP addresses**.
* If you are outside the U.S., you will need a **VPN with a U.S. server** to access them.

#### **Recommended People Search Engines**

1. **FastPeopleSearch**
   **Website:** [https://www.fastpeoplesearch.com/](https://www.fastpeoplesearch.com/)

   * Free to use (with ads).
   * Blocks non-U.S. IPs — **use a VPN**.

2. **Nuwber**
   **Website:** [https://nuwber.com/](https://nuwber.com/)

   * Good for finding phone numbers & relatives.
   * Blocks non-U.S. IPs — **use a VPN**.

3. **FastBackgroundCheck**
   **Website:** [https://www.fastbackgroundcheck.com/](https://www.fastbackgroundcheck.com/)

   * Searches across public records, court documents, and address history.

4. **ThatsThem**
   **Website:** [https://thatsthem.com/](https://thatsthem.com/)

   * Provides free access to addresses, emails, and phone numbers.

5. **Radaris**
   **Website:** [https://radaris.com/](https://radaris.com/)

   * Offers deeper reports (sometimes paid).

### **2.4 Uncover Political Party Affiliations**

**Voter Records**
These databases store registered voters’ details in certain U.S. states.

**Each record may include:**

* Full name
* Party affiliation
* Home address
* Date of birth
* Relatives

**Websites:**

1. [voterrecords.com](https://voterrecords.com/)
2. [voteref.com](https://voteref.com/)
3. [blackbookonline.info – USA Voter Records](https://www.blackbookonline.info/USA-Voter-Records.aspx)

**Usage Notes:**

* Best for **U.S. citizens only** — data availability varies by state.
* Use a **VPN with a U.S. IP** if blocked.

---

### **2.5 Finding Partners and Maiden Names in Registries**

**What is a Registry?**
A registry is a public (or semi-public) list where people share gift preferences for life events like weddings, baby showers, or birthdays. These can reveal:

* Partner’s name
* Maiden name
* Event date
* Desired items (can give clues about lifestyle, location, or wealth level)

#### **Websites & Usage**

1. **Amazon Baby Registry** – [amazon.com/baby-reg/search-results](https://www.amazon.com/baby-reg/search-results)

   * Use it to search for expectant parents by **name or city**.
   * Change `.com` to `.uk`, `.in`, etc. for your country’s Amazon site.

2. **Amazon Wedding Registry** – [amazon.com/wedding/search](https://www.amazon.com/wedding/search)

   * Search couples by **first and last names**.
   * Works internationally by changing the domain extension to match the country.

3. **MyRegistry** – [myregistry.com/search](https://www.myregistry.com/search/)

   * Aggregates baby, wedding, and other event registries from multiple retailers.

4. **The Knot – Wedding Registry Search** – [theknot.com/registry/couplesearch](https://www.theknot.com/registry/couplesearch)

   * Search for engaged couples by **first name, last name, and wedding month/year**.

5. **Target Registry** – [target.com/registry-kiosk](https://www.target.com/registry-kiosk)

   * Search by name and event type for **baby showers, weddings, birthdays**, etc.

### Summary
- Use search engines to find the person by their name and city.
- Learn where the name comes from.
- Search in people search engines.
- See if they're in voter records.
- Search in wedding/baby records.

## **2. Email OSINT**

### **2.1 Finding Email Addresses**

#### **1. Uncovering Emails from Social / Online Accounts**

* Check if the target has publicly shared their email on social media profiles or websites.
* Visit all found accounts and manually look for email addresses (e.g., in bio, “About” section, contact info).

#### **2. Using Search Operators**

* Use search engines to find publicly indexed email addresses.
  **Example query:**

```
"target name" "@hotmail.com" OR "@gmail.com" OR "@yahoo.com"
```

* Replace `"target name"` with their full name, username, or alias.

#### **3. Guessing Possible Email Addresses**

* Use **collected usernames** from the target’s profiles to create possible email combinations:

```
Collected usernames:
  user_name
  username420
  U.name
```

* Possible email guesses:

```
user_name@gmail.com
username420@yahoo.com
u.name@hotmail.com
```

#### **4. Validating Emails**

* Use an **email verification tool** like:
  🔗 [https://www.experte.com/email-finder](https://www.experte.com/email-finder)

  * Enter the guessed or found email.
  * Check if it’s **valid**.

#### **5. Confirming Ownership**

* If valid, verify if it belongs to the target:

  * Use **“Forgot Password”** feature on platforms like Facebook, Instagram, or Twitter.
  * Observe partial recovery info shown (phone digits, linked email).

  * Send a **test email** (without suspicious content) and check the display name in the reply or “To:” field.

#### **2.1.1 Creating and Verifying Possible Email Addresses**

* Generate a list of possible email combinations using the target’s name, username, or known aliases.
  **Example:**
  Name: *raju don*

```
rajudon@example.com  
raju@example.com  
```

* Use [Email Permutator](http://metricsparrow.com/toolkit/email-permutator/) to automatically generate all possible email variations.
* To verify:

  1. Paste all generated emails in the **To:** field of your email client to check for valid formatting.
  2. Remember: many emails avoid special characters like `_` or `-` and usually have 3–4 characters before the domain.

#### **2.1.2 Uncovering Emails with Browser Tools**

##### **Email Lookup Extensions**

Some browser extensions can reveal emails linked to social media accounts (especially LinkedIn):

* [ContactOut](https://chromewebstore.google.com/detail/email-finder-by-contactou/jjdemeiffadmmjhkbbpglgnlgeafomjo)
* [SignalHire](https://chromewebstore.google.com/detail/signalhire-find-email-or/aeidadjdhppdffggfgjpanbafaedankd)
* [GetProspect](https://chromewebstore.google.com/detail/email-finder-getprospect/bhbcbkonalnjkflmdkdodieehnmmeknp)

##### **Finding Business Emails**

* Identify company email patterns manually or with [Hunter.io](https://hunter.io/dashboard).
  **Example Patterns:**

  ```
  f.lastname@example.com  
  s.raju@example.com  
  ```
* If you need bulk company emails, use: [Phonebook.cz](https://phonebook.cz/)

#### **2.1.3 Discovering Emails Within Data Breaches**

Search in leaked/breached databases for email addresses linked to your target.

Search by:

* Name
* Phone Number
* Username

Check specific leaks if applicable:

* Facebook data leak → search by name/ID
* LinkedIn data breach → search by profile name/ID
* Twitter/X data leak → search by username or email

**Useful Breach Search Tools:**

* DeHashed
* LeakPeek
* BreachDirectory

### Summary
- Check if the email is **shared online.**
- Use **Google** Operators
- Form emails with username
- Utilize **Pasword Resets** to guess/verify an email.
- Use email **permutators**
- Use browser **extensions**
- Search in **Leaked** databases
- Identify an email **pattern**

### 2.2 Email OSINT - Discovering Info Linked to an Email Address 

### 1. Tracking the Identity Behind an Email Address 

**You'll learn how to:**
- Find information associated with any email address.

### Search Operators
Use search operators to check if an email address is indexed by seach engins.
```
"name@gmail.com"
```


### 2. Leveraging Password Resets to Validate Email Addresses 
Helps you find parts of an email address, potentially aiding in the process of **guessing** or **verifying** it.

```
example@gmail.com
|
e******@g****.com
```

### 3. Investigating an Email Address for Red Flags 

[emailrep.io](https://emailrep.io/) is a service that provides repution scores and information about email addresses.

**Reputation factors:**
- Presence on social media sites
- Public records
- Email deliverability
- Data breaches and credential leaks


### **4. Uncovering Websites & Accounts Linked to an Email Address**

If you know someone’s email, you can investigate whether it’s registered on different websites or social media platforms you didn’t initially identify. This is useful for discovering hidden accounts.

#### **Tools for Email-Based Account Discovery**

* **[Epieos](https://epieos.com/)** – Free tool that reveals whether an email is linked to accounts on multiple platforms. Also can find google reviews
* **[Castrick Clues](https://castrickclues.com/)** – Helps in finding accounts tied to an email across various services.
* **[PredictaSearch](https://www.predictasearch.com/)** – Paid tool, but it shows where an email may be registered (great for investigative leads).
* [Gravatar Email Check](https://gravatar.com/site/check)
 – Check if an email has a linked Gravatar profile. Sometimes it exposes the user’s full name, username, or even profile picture.

#### **Law Enforcement Use**

* In professional/law enforcement investigations, these tools can reveal the platforms an email is registered on.
* Once identified, investigators can **legally request** additional details from the platform (such as IP logs, last login time, or activity).

### **6 Discovering More Websites Linked to an Email Address**

Sometimes, free tools won’t uncover everything. Paid services exist that can search across hundreds of platforms for accounts tied to a specific email.

#### **Tool: OSINT Industries**

**Website:** [https://www.osint.industries/](https://www.osint.industries/)

* **Coverage:** Searches across **300+ websites** to identify accounts linked to an email.
* **Output:** Provides a list of platforms where the target email is registered.
* **Benefit:** Saves time compared to manual lookups on individual sites.

**Note:**

* This is a **paid service**.
* If you are working in **law enforcement or investigative roles**, you may be eligible for **free or discounted access**.

### **7 Gmail OSINT – Discovering Phone Numbers, Reviews, Addresses & More**

If the target uses **Gmail**, you can uncover valuable information such as:

* Partial phone number
* GAIA ID (Google’s internal user ID)
* Google Maps reviews
* Profile picture & activity

**Note:**
If you work in **law enforcement**, simply having the Gmail address or linked Google reviews is enough to request further information directly from Google.


#### **Manual Method – Finding GAIA ID**

1. Go to **Google Hangouts / Chat**: [https://mail.google.com/chat/u/0/#chat/home](https://mail.google.com/chat/u/0/#chat/home)
2. Enter the target’s **email address**.
3. Open **Inspect (Ctrl+Shift+I)**.
4. Go to **Network tab**.
5. Refresh the page.
6. Search for **`GetAssistiveFeatures`**.
7. Click on it → open **Response tab**.
8. Look for **GAIA ID** inside the response.
9. Copy the GAIA ID.
10. Use it in this format:

```
http://www.google.com/maps/contrib/GAIA_ID
Example: http://www.google.com/maps/contrib/101081729873
```

11. Open in browser → You can see the target’s **Google Maps reviews, photos, or activity**.

#### **Automated Method – GHunt**

**GHunt** is a tool designed to gather information from Gmail accounts.

* **Online Access:** [GHunt Online](https://gmail-osint.activetk.jp/)
* **Linux Tool:** Can be downloaded & run locally for deeper analysis.

 **Information GHunt Reveals:**

* Profile picture
* GAIA ID
* Last profile update date
* Linked Google services
* Public Google Maps reviews

 Tip: Always cross-check GAIA ID results with other Google services like **YouTube, Maps, Photos** – sometimes they reveal more than expected.

### **8 Leveraging Usernames and Emails to Discover Additional Accounts**

Sometimes, a username or email address is reused across different platforms. You can take advantage of this to discover hidden or linked accounts.

#### **Tool: Blackbird**

**GitHub:** [https://github.com/p1ngul1n0/blackbird](https://github.com/p1ngul1n0/blackbird)

**Platform:** Linux

**Key Features:**

*  Reverse **username search** across **700+ websites**
* Reverse **email search** across **10+ platforms**
* Supports **AI-powered metadata extraction** for deeper analysis

 **Use Case:**

* Find hidden accounts on forums, social media, or niche websites.
* Correlate one identity across multiple platforms.
* Cross-verify email or username usage patterns.

### Email Osint Recap

- Check email presence on **Search engines.**
- Assess email **reputation.**
- Identify **email registations** on other sites.
- Search in data **leaks/breaches.**
- Try **password reset.**
- Conduct reverse email lookup uing **SignalHire.  **

--- 

## Phone Number OSINT
You'll learn how to:
- Find Someone's **Phone Number.**

Note: Findint a phone number is more difficult than finding an email.

Having an email makes it easier to find a phone number.

### 1. Check Online Accounts
Check if the person has shared their phone number on their online/social media accounts.

#### Search Operators
Use **search operators** to find the person's phone number on search engins.

**Search operator:**
```
"first and last name" "city" "phone number" OR "number" OR "country code"
```

### 2. Uncovering Phone Numbers Linked to Linkedin Accounts

Some browser extensions allow you to find a phone number associated to a Linkedin account.

* [ContactOut](https://chromewebstore.google.com/detail/email-finder-by-contactou/jjdemeiffadmmjhkbbpglgnlgeafomjo)
* [SignalHire](https://chromewebstore.google.com/detail/signalhire-find-email-or/aeidadjdhppdffggfgjpanbafaedankd)
* [GetProspect](https://chromewebstore.google.com/detail/email-finder-getprospect/bhbcbkonalnjkflmdkdodieehnmmeknp)

Note: 
- It's already covered in LinkedIn Osint
- Search for the person's info in leaked/breached databased.

### **3. Uncovering Detailed Phone Number Information**

**Phone number lookup** is the process of finding general information about a phone number.
It helps you gather technical and geographical details, even without contacting the owner.

**Information you can discover:**

*  **Number type** (mobile, landline, VoIP)
* **Service provider** (carrier/telecom company)
* **Spam score** (if reported for fraud/scam)
* **Location / Region** (approx. origin of the number)

#### **Useful Tools & Websites**

1. **IPQualityScore** – [Free HLR Lookup](https://www.ipqualityscore.com/free-hlr-lookup)

   * Checks if number is valid, active, and its carrier info.

`2. **Comfi** – [Reverse Phone Lookup](https://www.comfi.com/abook/reverse)

   * Simple reverse search for international numbers.

3. **NumberingPlans** – [Phone Number Analysis](https://www.numberingplans.com/index.php?page=analysis&sub=phonenr)

   * Identifies format, operator, and origin.

4. **SearchYellowDirectory** – [Directory Search](https://www.searchyellowdirectory.com/)

   * Works like a digital phone book.

5. **PhoneValidator** – [Validator](https://www.phonevalid`ator.com/) *(US only)*

   * Checks if number is valid, carrier, and type (mobile/landline/VoIP).

6. **NPANXX Source** – [NPA-NXX Lookup](https://www.npanxxsource.com/nalennd.php) *(US & Canada)*

   * Provides detailed **exchange-level info** for North American numbers.

### 4. Revealing Sensitive Information Using Advanced Search Techniques

### Search Operators

Search engines can reveal if a phone number is indexed online. Different formats should be tested because numbers are posted in various ways.

**International Format:**

```
"+CCXXXXXXXXXX" OR "00CCXXXXXXXX" OR "CCXXXXXXXXXX" OR "XXXXXXXXXXX"
```

* **CC** = Country Code (e.g., +91 for India, +1 for USA).

**US Format:**

```
"XXXXXXXXXX" OR "XXX-XXX-XXXX" OR "XXX.XXX.XXXX" OR "XXX XXX XXXX"
```


### Caller ID Identifiers

These tools help identify unknown numbers, such as spam calls or real owners.

* [Truecaller](https://www.truecaller.com/)
* [Sync.me](https://sync.me/)
* [Numlookup](https://www.numlookup.com/)
* [Spydialer](https://www.spydialer.com/)
* [CallerID Test](https://calleridtest.com/)
* [Old Phonebook](https://oldphonebook.com/)

### People Search Engines (US-based)

Useful for gathering information like names, addresses, and background data. Most of these are limited to US residents, so a **US VPN** is recommended.

* [TruePeopleSearch](https://www.truepeoplesearch.com/)
* [FastBackgroundCheck](https://www.fastbackgroundcheck.com/)
* [ThatsThem](https://thatsthem.com/)
* [Nuwber](https://nuwber.com/)
* [IntelTechniques Phone Tools](https://inteltechniques.com/tools/Telephone.html)

### Workflow Example

1. Use Google search operators to check if the number appears online.
2. Use Caller ID tools to identify the owner or spam status.
3. If needed, pivot to People Search Engines (with a US VPN).
4. Verify results and organize findings into a report.
Here’s a refined version of your notes, kept simple, clear, and consistent with the previous section.

## 5. Uncovering Accounts Registered with a Phone Number

Some OSINT tools allow you to check whether a phone number is linked to online accounts.

**Tools and Resources:**

* [Epieos](https://epieos.com/)
* [Castrick Clues](https://castrickclues.com/)
* [OSINT Industries](https://www.osint.industries/)

**Other Methods:**

* **SignalHire Extension** → Find LinkedIn accounts connected with a phone number.
* **Database leaks/breaches** → Check if the number has appeared in leaks.

  * Example: [HaveIBeenZuckered](https://haveibeenzuckered.com/) (Facebook Data Breach Checker).

## Deep Phone Number Scanning & Footprinting

### Phoneinfoga

[Phoneinfoga](https://sundowndev.github.io/phoneinfoga/getting-started/install/) is a powerful OSINT tool to analyze phone numbers.

**Features:**

* Validate if a phone number is active/valid.
* Collect basic information (carrier, location range, type).
* Provide Google Dorks for further searching.
* Check reputation reports (spam/scam tags).

### Phone OSINT Recap
- Use search operators.
- Use caller ID identifiers.
- Seach in people search engines.
- Identify phone registations on other sites.
- Conduct reserse phone lookup using SignalHire.
- Search in data leaks/breaches.

---

## Image OSINT
You'll learn how to:
- Find information about an image or a picture.

### 1. Gathering Profile Images for OSINT Investigations

#### Downloading Profile Pictures
- Download unique profile picture from gathered online accounts.
- Use these pictures to find accounts.

### 2. Tracking Images Using Google

#### Reverse Image Search

Reverse Image Search is a technique that allows you to search the internet using an **image instead of text**.

**Uses in OSINT:**

* Verify image authenticity (detect edits or fake images).
* Identify the original source of an image.
* Find visually similar content online.

#### Google Reverse Image Search

* [Google Images](https://www.google.com/imghp?hl=en&ogbl) allows searching for an image across the web.

**Features:**

* Shows websites where the image appears.
* Can detect single objects in an image.

**Extensions:**

* [Search by Image (Firefox)](https://addons.mozilla.org/en-US/firefox/addon/search_by_image/)
* [Search by Image (Chrome)](https://chromewebstore.google.com/detail/search-by-image/cnojnbdhbhnkbcieeekonklommdnndci?hl=en)

#### Bing Reverse Image Search

* [Bing Image Search](https://www.bing.com/)

**Features:**

* Finds visually similar images.
* Strong object detection.
* Effective for detecting **products and items** in images.

#### Yandex Reverse Image Search

* [Yandex Images](https://yandex.com/images/)

**Features:**

* Strong facial recognition (good for finding similar faces).
* Can identify certain locations.
* Strong text recognition.
* Useful "Recognize Text" feature for extracting text from images.

#### Other Image Search Engines

* [Numlookup Reverse Image Search](https://www.numlookup.com/reverse-image-search)
* [TinEye](https://tineye.com/)

### 3. Track Online Presence/Profiles Using a Photo

### Facial Recognition

Facial recognition tools allow you to search the internet for **identical or similar faces** that may appear online.

**Tools:**

* [Search4Faces](https://search4faces.com/)
* [PimEyes](https://pimeyes.com/en)
* [FaceCheck](https://facecheck.id/)
* [CyberChef](https://gchq.github.io/CyberChef/) (used for analyzing/manipulating images and data)

### 4. Image OSINT – Geo Location Tracking

### Finding Where a Photo Was Taken

Always attempt to determine **where an image was captured** using context clues, AI tools, or metadata.

### Using AI for Geolocation

**[GeoSpy](https://geospy.ai/)** is an AI-powered tool that can estimate where a picture was taken.

It analyzes:

* Landmarks
* Vegetation
* Building styles

### Metadata Analysis

**Metadata** = extra information stored inside images, videos, or documents.

**Common Metadata Fields:**

* Creation and modification dates
* Author or username
* GPS coordinates (location where the photo was taken)
* Device information (camera/phone model, software)

**Note:**

* Platforms like **Instagram** and **Facebook** strip (remove) metadata from uploaded photos.
* Some websites do not remove metadata, so files may still contain GPS or device info.

**Tools:**

* [EXIF Tools](https://exif.tools/)
* [Metadata2Go](https://www.metadata2go.com/)

**Extensions:**

* [EXIF Viewer (Firefox)](https://addons.mozilla.org/en-US/firefox/addon/exif-viewer/)

---

## Map OSINT

### Google Maps

[Google Maps](https://www.google.com/maps/) has extensive global coverage, making it the most widely used mapping service worldwide.

**Features:**

* Street View
* Local business information
* Real-time traffic data

---

### Bing Maps

[Bing Maps](https://www.bing.com/maps) also offers strong global coverage.

**Features:**

* Bird’s Eye View
* Displays data from other sources

---

### Yandex Maps

[Yandex Maps](https://yandex.com/maps/) is especially strong in Russia and former Soviet countries.

**Features:**

* Metro maps
* Real-time public transport info
* Local business information

---

### Other Mapping Sites

* [Satellites.pro](https://satellites.pro/) → Switch between Google, Apple, and Yandex maps.

---

### Street-Level Imagery

* [KartaView](https://kartaview.org/landing)
* [Mapillary](https://www.mapillary.com/)

**Features:**

* Community-contributed imagery
* Frequently updated
* Provides extra coverage in areas not covered by Street View

---

### Geo-Locating Images Using OpenStreetMap (OSM)

**Bellingcat OSM Tool:**

* [Bellingcat OSM Search](https://osm-search.bellingcat.com/)
* Helps find landmarks and features in photos using **OpenStreetMap** data.

**Guides:**

* [Finding Geolocation Leads](https://www.bellingcat.com/resources/how-tos/2023/05/08/finding-geolocation-leads-with-bellingcats-openstreetmap-search-tool/)

**Other:**

* [Google Earth](https://www.google.com/earth/about/versions/) for 3D mapping and terrain analysis.

---

## Website OSINT

### 1. Discovering Website Owners & Hidden Contact Details

**WHOIS Records:**

* Public database showing domain ownership.
* Includes:

  * Owner’s name and contact details
  * Registration & expiration dates
  * Domain registrar information

**Tools:**

* [Who.is](https://who.is/)
* [Reverse WHOIS](https://osint.sh/reversewhois/)
* [Reverse Domain](https://osint.sh/domain/)

---

### 2. Identifying Website Technologies

**Why:** Helps understand a website’s infrastructure and possible vulnerabilities.

**Data you can find:**

* CMS (Content Management System)
* LMS (Learning Management System)
* Plugins, frameworks, servers

**Tools:**

* [osint.sh Stack](https://osint.sh/stack/)
* [Wappalyzer (Chrome)](https://chromewebstore.google.com/detail/wappalyzer-technology-pro/gppongmhjkpfnbhagpmjfkannfbllamg)
* [Wappalyzer (Firefox)](https://addons.mozilla.org/en-US/firefox/addon/wappalyzer/)

---

### 3. Discovering Subdomains

**Definition:** A subdomain is a prefix added to the main domain (e.g., `academy.example.org`).

**Tools:**

* [Subdomain Finder](https://osint.sh/subdomain/)
* [crt.sh](https://crt.sh/)

---

### 4. Extracting Information From DNS Records

**DNS Records:** Instructions stored in DNS servers providing information about a domain.

**Tools:**

* [DNSDumpster](https://dnsdumpster.com/)
* [DNS History](https://osint.sh/dnshistory/)
* [ViewDNS](https://viewdns.info/)

---

### 5. Uncovering Websites Under Same Ownership

**Google Analytics ID:**

* A unique identifier that can reveal multiple sites owned by the same person/org.

**Tools:**

* [DNSlytics Reverse Analytics](https://dnslytics.com/reverse-analytics/)
* [HackerTarget Reverse Analytics](https://hackertarget.com/reverse-analytics-search/)

---

### 6. Tracking Website Changes & Updates

**Wayback Machine:**

* [Archive.org](https://archive.org/)
* Contains 800+ billion archived web pages.

**OSINT Uses:**

* View websites as they looked in the past
* Retrieve deleted information
* Track content changes over time

---

### 7. Investigating Website Files

**FOCA Tool:**

* Downloads, extracts, and analyzes metadata from documents published on a domain.

**Features:**

* Collect public documents
* Extract metadata (author, software, timestamps)
* Metadata analysis

**Downloads:**

* [FOCA GitHub](https://github.com/ElevenPaths/FOCA)
* [.NET Framework 4.7.1](https://dotnet.microsoft.com/en-us/download/dotnet-framework/net471)
* [Microsoft Download 1](https://www.microsoft.com/en-us/download/details.aspx?id=26999)
* [Microsoft Download 2](https://www.microsoft.com/en-us/download/details.aspx?id=42299)

---

## OSINT Reporting

### Relationship Map

* [OSINTracker](https://www.osintracker.com/) → Create OSINT relationship maps.

### OSINT Flowcharts

* Visualize steps of an OSINT process.
* Ensure no investigation steps are missed.

**Resources:**

* [IntelTechniques OSINT Book](https://inteltechniques.com/osintbook/)
* [Yoga OSINT Training](https://yoga.myosint.training/)

---

### Writing an OSINT Report

**Purpose:**
Present structured open-source findings to a client or team.

**Report Should Include:**

* Scope
* Summary
* Key Findings
* Verification Steps
* Supporting Evidence
* Recommendations

``