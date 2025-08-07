---
title: 'OSINT '
updated: 2025-08-07 05:19:22Z
created: 2025-08-04 12:58:51Z
latitude: 23.06858650
longitude: 72.65359610
altitude: 0.0000
tags:
  - osint notes
---

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

![Account creation dates.png](../_resources/Account%20creation%20dates.png)

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

### Let's Recap

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

### 2.1 Intro of Instagram

<span style="color: rgb(252, 176, 69);">Instagram </span>has over 1 billion monthlyactive users.
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

1. Go to the **target Instagram post or comment**.
2. Right-click the **post time/date** (e.g. *“8w”*, *“19 April”*).
3. Click **"Inspect"** (or press `Ctrl + Shift + I`).
4. In the source code, locate the `<time>` tag.
5. Copy the `datetime` value:
   `2025-04-19T16:52:04.000Z` 
6.  Go to: [timestamp-converter.com](https://www.timestamp-converter.com/)
7. Paste the timestamp into the converter.
8. You will see the **exact local time** in your time zone.

### 2.4 Uncovering Comments of Private Instagram Accounts 

Utilize search engine operators to discover indexed information on instagram profiles.

```url
site:instagram.com "Username"
site:instagram.com "@Username"
site:twitter.com "username" "instagram.com/p"
```

- You can direct paste Profile URL: 
`https://www.instagram.com/username/` on google, bing, yandex search bar and got result like where user liked, comment, posts etc.
Absolutely, Falcon 🦅 — here’s your cleaned-up, professional, and **note-friendly** version of:


###  2.5 Extracting Hidden Information from Instagram Metadata

###  **What is Instagram Metadata?**

**Account Metadata**
- **Metadata** can something contain useful information
- **Browser Extention:** User-Agent Switcher and Manager

**Metadata** refers to hidden or background information embedded within content or served through APIs — such as device type, operating system, full-size profile pictures, and sometimes extra details not shown on the main app or website.

Instagram’s web interface **hides some data** unless it thinks you’re using a mobile device.
We can bypass this by **changing the browser’s user agent** to mimic an Android device.

###  **Tools You Need**

To do this, use a browser extension like:

* 🔹 [User-Agent Switcher and Manager – Chrome](https://chromewebstore.google.com/detail/user-agent-switcher-and-m/bhchdcejhohfmigjafbampogmaanbfkg)
* 🔹 [User-Agent Switcher and Manager – Firefox](https://webextension.org/listing/useragent-switcher.html?version=0.6.4&type=install)

### **How to Use (Step-by-Step)**

1. Go to the target's **Instagram profile**.
2. Open the **User-Agent Switcher and Manager** extension.
3. Select:

   * **Device**: Android
   * **Site**: Instagram
   * **User Agent**: Choose any Android browser
4. Click **Apply (All Tabs)** — this sets your browser to act like a mobile device.

### **Accessing Metadata**

Now you’re ready to pull hidden details using Instagram’s mobile endpoint.

#### Use this URL format:

```url
https://i.instagram.com/api/v1/users/USER_ID/info/
```

* Replace `USER_ID` with the **actual user ID** of your target. (e.g. 49279209744)
* Example:
  `https://instagram.com/49279209744/`

Open the link in your browser **with the mobile user agent active**.


### **Why This Is Useful**

* Normally, when you try to download someone’s **Instagram profile picture**, it gives you a **low-res 320×320** version.
* But when accessing the profile with a **mobile user agent**, Instagram serves the **HD version** of the profile picture — often up to **1080×1080 or higher**.

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
1. Press F5
2. Click on **special**
3. Select objects
4. click OK
5. Press Delete key on keyboard

##  **Filtering URL and Display Name in Excel**

1. **Select the column** where your data is stored (e.g., Column A).
2. Go to the **`Data`** tab in the top menu.
3. Click on **`Filter`**.
4. A small **dropdown arrow (▼)** will now appear next to the column name (e.g., A1).
5. Click on the dropdown arrow.
6. Choose:

   * **"Filter by Color"** – if you’ve highlighted rows.
   * **"Text Filters"** – to filter by keywords like "facebook.com", "gmail", or names.

## **Get Instagram Followers Data Using Extension**

Instead of manually scrolling and copying follower lists, use a browser extension to **extract and export Instagram follower data** efficiently.

> ⚠️ **Important:**
> Always use a **puppet (fake) account** when using automation tools. Instagram may detect this activity and **ban or restrict your account**.


### **Extension Used**

🔗 [**IG Follower Export Tool - IG Tools** (Chrome)](https://chromewebstore.google.com/detail/ig-follower-export-tool-i/kicgclkbiilobmccmmidfghnijgfamdb)

### **Steps to Use the Extension**

1. Log in to **Instagram** using your **puppet account**.
2. Go to the **target user’s profile**.
3. Click the **IG Follower Export Tool** extension icon in your browser.
4. Click **“Export Instagram Data”**.
5. In the input field, enter the **Instagram handle** or full profile URL:
   Example: `@username` or `https://www.instagram.com/username`
6. Increase the **delay time** (e.g., `10s`) to avoid detection or temporary blocks.
7. Click **“Start New Parsing”** to begin scraping the follower list.
8. After the process completes, click **“Save to Excel”** to download the data.

 **Output includes:**  ID, username, name, profile URL, avatar, verification, follow status
Absolutely, Falcon 🦅 — here's your cleaned-up, properly formatted, and **OSINT-friendly** version of:

## 2.7 Downloading Instagram Posts

Whether you're archiving a target's content for OSINT, digital profiling, or offline analysis, there are **two ways** to download Instagram images: manually or using browser extensions.

### **Manual Method (One Post at a Time)**

Use this when you only need to download **a few images**:

1. Go to the **Instagram post**.
2. Right-click on the page and click **Inspect** (or press `Ctrl + Shift + I`).
3. Locate and **select the image element** (inside the HTML code).
4. Copy the **image URL** from the `src` attribute.
5. Paste the URL in a **new browser tab**.
6. Right-click and **save the image**.

> ⚠️ This method is time-consuming if the user has **many posts**.

### **Browser Extension Method (Bulk Download)**

If the account has **dozens or hundreds of posts**, use a tool like:

🔗 [**Download All Images – Chrome Extension**](https://chromewebstore.google.com/detail/download-all-images/nnffbdeachhbpfapjklmpnmjcgamcdmm?hl=en)

### **Steps to Use the Extension:**

1. Go to the **target’s Instagram profile**.
2. **Scroll down** until **all the posts are loaded** (important!).
3. Click the **Download All Images** extension in your browser.
4. In the extension settings:

   * Select image type (e.g., `JPG`)
5. Wait for the extension to finish scanning the page.
6. Click **Save** — all images will be downloaded as a **ZIP file**.

### Notes:

* This works **only for public profiles**.
* For private accounts, you must be **following the target** with a valid or puppet account.
* Instagram might **rate-limit or throttle** image loads if you're scraping too fast — keep it human-like.

## 3. Creating an OSINT Virtual Machine 

### 3.1 Set up OSINT VM

**TraceLabs VM** is a customized version of kali Linux focused solely on OSINT tools.

**Why to use a Linux distribution?**
- Pre-configured Enviroment
- Tool Compatibility
 