# 12. Resetting User Passwords - Secure Implementation

When users forget their passwords, it's essential to provide a secure method for them to reset it. Since password-based authentication is impossible in this scenario, websites rely on alternative verification methods to ensure the legitimate user is resetting their own password.

⚠️ **Warning:** Password reset functionality is inherently dangerous and must be implemented securely to prevent exploitation.

---

## 1️⃣ Sending Passwords by Email

❌ **What NOT to do:**

Sending users their current password should **never** be possible if passwords are handled securely.

✅ **What some sites do instead:**

Generate a new password and send it to the user via email.

⚠️ **Security risks:**

- Sending persistent passwords over insecure channels (like email) is unsafe.
- Security relies on the new password either **expiring quickly** or the user **changing it immediately**.
- If not, this approach is highly vulnerable to **man-in-the-middle (MITM) attacks**.

📧 **Why email is problematic:**

- Email inboxes are **persistent** and not designed for secure storage of sensitive data.
- Many users sync their inboxes across multiple devices, sometimes over **insecure channels**.

---

## 2️⃣ Resetting Passwords Using a URL

### a) **Insecure Implementation**

Example URL with easily guessable user parameter:

```html
http://vulnerable-website.com/reset-password?user=victim-user
```

⚠️ **Risk:**

An attacker can change the `user` parameter to any known username and be taken directly to a page where they can reset that user's password — bypassing any verification.

---

### b) **Improved Implementation with Token**

Example URL with a high-entropy, hard-to-guess token:

```html
http://vulnerable-website.com/reset-password?token=a0ba0d1cb3b63d13822572fcff1a241895d893f659164d4cc550b421ebdd48a8
```

✅ **Best practice:**

- Generate a **unique, high-entropy token** for each password reset request.
- The URL should reveal **no information** about the user's identity.
- When the user visits the URL, the system:
    - Validates the token on the backend.
    - Identifies which user's password can be reset using this token.
- The token should **expire after a short time** and be **destroyed immediately** after use.

---

### c) **Common Pitfall**

❌ Some implementations **fail to validate the token again when the password reset form is submitted**.

⚠️ **Exploit scenario:**

- An attacker visits the reset form using their own valid token.
- They delete the token from the server.
- Then they use this form to reset the password for an arbitrary user, bypassing token validation entirely.

---

# 🎯 **Summary of Secure Password Reset Implementation**

| Step | Secure Practice |
| --- | --- |
| Token Generation | Use **high-entropy**, hard-to-guess tokens with no user info in URL |
| Token Validation | Validate the token **both on link visit and form submission** |
| Token Expiry | Tokens should have a **short lifespan** and be **invalidated immediately after use** |
| Email Transmission | Avoid sending passwords via email; instead, send reset **links only** |
| User Identification | Token should be the sole identifier, not usernames or emails in URL parameters |
| Secure Storage | Passwords must be stored hashed — never sent or stored in plaintext |