# 3. How does CSRF work?

### 🔑 **For a CSRF attack to be possible, three key conditions must be in place:**

---

### 1️⃣ **A relevant action**

There is an action within the application that the attacker has a reason to induce.

This might be:

- A privileged action (such as modifying permissions for other users)
- Any action on user-specific data (such as changing the user's own password)

---

### 2️⃣ **Cookie-based session handling**

- Performing the action involves issuing one or more HTTP requests
- The application **relies solely on session cookies** to identify the user who has made the requests
- There is **no other mechanism** in place for tracking sessions or validating user requests

---

### 3️⃣ **No unpredictable request parameters**

- The requests that perform the action **do not contain any parameters** whose values the attacker cannot determine or guess
- Example: When changing a user's password, if the attacker **needs to know the old password**, the function is not vulnerable

---

### 🧪 **Example Scenario**

Suppose an application contains a function that lets the user change the email address on their account.

When a user performs this action, they make an HTTP request like the following:

```
POST /email/change HTTP/1.1
Host: vulnerable-website.com
Content-Type: application/x-www-form-urlencoded
Content-Length: 30
Cookie: session=yvthwsztyeQkAPzeQ5gHgTvlyxHfsAfE

email=wiener@normal-user.com
```

---

### ✅ **This meets the conditions required for CSRF:**

- **Relevant action:**
    
    The action of changing the email address on a user's account is of interest to an attacker.
    
    Following this action, the attacker will typically be able to trigger a password reset and take full control of the user's account.
    
- **Cookie-based session handling:**
    
    The application uses a session cookie to identify which user issued the request.
    
    There are no other tokens or mechanisms in place to track user sessions.
    
- **Guessable parameters:**
    
    The attacker can easily determine the values of the request parameters that are needed to perform the action.
    

---

### ⚠️ **Attack Page Example**

The attacker can construct a web page containing the following HTML:

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

---

### 🧬 **If a victim user visits the attacker's web page, the following will happen:**

1. The attacker's page will trigger an HTTP request to the vulnerable website.
2. If the user is logged in to the vulnerable website, their browser will **automatically include their session cookie** in the request (assuming Same Site cookies are not being used).
3. The vulnerable website will process the request in the normal way, treat it as having been made by the victim user, and **change their email address**.

---

> **Note**
> 
> 
> Although CSRF is normally described in relation to cookie-based session handling, it also arises in other contexts where the application automatically adds some user credentials to requests, such as **HTTP Basic authentication** and **certificate-based authentication**.
>