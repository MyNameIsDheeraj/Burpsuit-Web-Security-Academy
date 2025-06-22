# 12. CSRF token is tied to a non-session cookie

## 🔐 Basic Concept: CSRF Protection

Normally, CSRF tokens work by:

1. Server generates a random token.
2. Token is:
    - **Stored in the user’s session** on the server.
    - **Sent to the client** (usually embedded in forms or JavaScript).
3. When the user submits a form (like changing their email), the server:
    - Compares the CSRF token in the request body with the one stored in the session.
    - If it matches, the request is allowed.

This helps stop a malicious site from forging authenticated actions on behalf of a logged-in user.

## ❌ Vulnerable Setup (Exploit Scenario)

Now, consider this bad setup:

### 📋 Request Example:

```
POST /email/change HTTP/1.1
Host: vulnerable-website.com
Content-Type: application/x-www-form-urlencoded
Cookie: session=pSJYSScWKpmC60LpFOAHKixuFuM4uXWF; csrfKey=rZHCnSzEp8dbI6atzagGoSYyqJqTz5dv

csrf=RhV7yQDO0xcq9gLEah2WVbmuFqyOq7tY&email=wiener@normal-user.com
```

There are **two cookies**:

- `session`: Tracks the user's login.
- `csrfKey`: Stores the CSRF token (but not tied to the session).

### 🧠 Problem:

The CSRF token is **tied to the `csrfKey` cookie**, **not** the `session` cookie.

So, validation works like this:

- Server checks if `csrf` value from form matches the `csrfKey` cookie.
- ✅ If it matches: request allowed.

BUT... this is bad design, because:

> Anyone who can set the csrfKey cookie in the victim’s browser can bypass CSRF protection.
> 

## 🎯 Exploit Idea: How an Attacker Can Abuse This

1. **Attacker logs in to their own account**, gets:
    - Their own `csrfKey` cookie value
    - Their own valid CSRF token
2. **Attacker finds a way to set cookies in the victim’s browser**.
    - For example: using a subdomain like `staging.example.com` which can set cookies for `.example.com`.
3. Attacker **sends victim a malicious link or auto-submitting form** that:
    - Submits the attacker's **valid CSRF token**
    - Browser sends **attacker's `csrfKey` cookie**
    - Session cookie is victim’s (they’re logged in as the target)
    - Server validates CSRF token **against attacker's cookie value**: ✅ Match.
4. Server performs action (e.g., changes victim’s email).

## 💡 Key Insight: Cookie Scoping

- Cookies set on a subdomain like `staging.example.com` **can have a domain scope of `.example.com`**, so they’re sent to `secure.example.com`.
- So even **unrelated apps** in the same domain can **set cookies for the vulnerable app**.

## 🔐 Why This Is Bad Design

- CSRF tokens should always be **tied to the session** or derived from it (e.g., HMAC with session ID).
- Relying on **a separate, non-session cookie** for CSRF protection breaks this assumption:
    - Anyone who can set that cookie can forge a valid CSRF request.

## ✅ How to Fix

- **Tie CSRF token to the session** — don’t use separate cookies for CSRF.
- **Use `SameSite` cookies** (preferably `SameSite=Lax` or `Strict`) to prevent cookies being sent in cross-origin requests.
- Avoid having **cookie-setting functionality** on subdomains unless properly sandboxed.

## 🧠 Summary

| Concept | Explanation |
| --- | --- |
| CSRF Token tied to non-session cookie | Token is matched against a cookie not tied to the session |
| Risk | Any app that can set that cookie can spoof a CSRF token |
| Exploit | Attacker sets their CSRF cookie + sends their token in request = CSRF bypass |
| Fix | Tie CSRF token to session, use `SameSite`, avoid shared cookie scope |

---