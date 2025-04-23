# Report Format

1. Vulnerability name
2. Vulnerability Description
3. Vulnerable URL
4. Payload Used - XSS,SQLi,SSRF
5. Impact
6. Steps to reproduce this vulnerability
    - Go to this URL:  
   `http://testphp.vulnweb.com/search.php?test=`
    - Capture the request in **Burp Suite**.
    - Send the request to the **Repeater** tab.
    - Add this XSS payload to the `test` parameter: `<script>alert(document.cookie)</script>`
    -  Send the request and observe the result in the response.
    - Copy the response, open it in a browser, and & open in a browser and, XSS is there.l

7. POC -Proof Of Concept {Screenshot/ Videos}
8. Remediation/ Recommendation/Countermeasur