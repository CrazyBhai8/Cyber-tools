# CSRF Cross-site request forgery 

## What is CSRF?
CSRF (Cross-Site Request Forgery) is a type of security vulnerability where an attacker tricks a user into performing unintended actions on a website they’re logged into. For example, clicking a malicious link might cause you to transfer money or change account settings without realizing it. It works because the website trusts the user's logged-in session, even though the action wasn’t intentional.

## How does CSRF work?
CSRF attacks happen when three main conditions are met:  

1. **An important action**: The attacker wants to trick the user into doing something significant, like changing a password, transferring money, or modifying account settings.  

2. **Session cookies are used**: The website identifies the user based only on cookies stored in their browser. It doesn’t ask for extra verification for actions.  

3. **Predictable requests**: The attacker can guess the details of the request needed to perform the action, such as knowing how the website processes a password change.  

If these conditions exist, the attacker can trick a logged-in user into unknowingly sending a harmful request.

# # CSRF Example

## How CSRF Works

### Scenario
Suppose an application allows users to change their email address. A user performs this action by sending the following HTTP request:

```
POST /email/change HTTP/1.1
Host: vulnerable-website.com
Content-Type: application/x-www-form-urlencoded
Content-Length: 30
Cookie: session=yvthwsztyeQkAPzeQ5gHgTvlyxHfsAfE

email=wiener@normal-user.com
```

### Conditions for CSRF

1. **Action of Interest**:
   The attacker wants to change the user's email address. This allows them to trigger a password reset and take full control of the user's account.

2. **Session Cookie Reliance**:
   The application identifies the user using a session cookie and has no other mechanisms, like CSRF tokens, to verify the request.

3. **Predictable Parameters**:
   The attacker knows the parameters needed for the request (e.g., the `email` field).

### Attacker's Exploit
The attacker creates a web page with the following HTML:

```html
<html>
    <body>
        <form action="https://vulnerable-website.com/email/change" method="POST">
            <input type="hidden" name="email" value="pwned@evil-user.net" />
        </form>
        <script>
            document.forms[0].submit();
        </script>
    </body>
</html>
```

### Steps of the Attack

1. **Victim Visits the Malicious Page**:
   When the victim user visits the attacker's page, the malicious script automatically triggers an HTTP request to the vulnerable website.

2. **Session Cookie Sent**:
   If the victim is logged in, their browser includes their session cookie in the request (assuming SameSite cookies are not being used).

3. **Request Processed**:
   The vulnerable website treats the request as coming from the victim and changes their email address to the attacker's email.

## Common Flaws in CSRF Token Validation

### CSRF Token Validation Depends on Request Method
Some applications validate the CSRF token for `POST` requests but skip validation for `GET` requests. This allows attackers to bypass the validation by switching to the `GET` method:

```
GET /email/change?email=pwned@evil-user.net HTTP/1.1
Host: vulnerable-website.com
Cookie: session=2yQIDcpia41WrATfjPqvm9tOkDvkMvLm
```

### CSRF Token Validation Depends on Token Presence
Some applications validate the token if it is present but skip validation if the token is missing. Attackers can remove the token parameter to bypass validation:

```
POST /email/change HTTP/1.1
Host: vulnerable-website.com
Content-Type: application/x-www-form-urlencoded
Content-Length: 25
Cookie: session=2yQIDcpia41WrATfjPqvm9tOkDvkMvLm

email=pwned@evil-user.net
```

### CSRF Token Not Tied to User Session
Some applications accept any valid token, even if it does not belong to the user making the request. Attackers can use their own account to obtain a valid token and feed it to the victim in a CSRF attack.

### CSRF Token Tied to a Non-Session Cookie

Sometimes, CSRF tokens are linked to a cookie that is different from the session cookie. This can happen when the application uses separate frameworks for session handling and CSRF protection. For example:

```
POST /email/change HTTP/1.1
Host: vulnerable-website.com
Content-Type: application/x-www-form-urlencoded
Content-Length: 68
Cookie: session=pSJYSScWKpmC60LpFOAHKixuFuM4uXWF; csrfKey=rZHCnSzEp8dbI6atzagGoSYyqJqTz5dv

csrf=RhV7yQDO0xcq9gLEah2WVbmuFqyOq7tY&email=wiener@normal-user.com
```

If attackers can find a way to set cookies in the victim’s browser (for example, through another application or subdomain), they can insert their own CSRF token and matching cookie to exploit the vulnerability.

---

### CSRF Token Simply Duplicated in a Cookie

In some cases, CSRF tokens are stored in both a request parameter and a cookie. During validation, the application just checks if these two values match, without keeping any server-side record of issued tokens. For example:

```
POST /email/change HTTP/1.1
Host: vulnerable-website.com
Content-Type: application/x-www-form-urlencoded
Content-Length: 68
Cookie: session=1DQGdzYbOJQzLP7460tfyiv3do7MjyPw; csrf=R8ov2YBfTYmzFyjit8o2hKBuoIjXXVpa

csrf=R8ov2YBfTYmzFyjit8o2hKBuoIjXXVpa&email=wiener@normal-user.com
```

An attacker can simply create their own fake CSRF token, set a matching cookie in the victim’s browser, and carry out a CSRF attack without needing a valid token from the application.
