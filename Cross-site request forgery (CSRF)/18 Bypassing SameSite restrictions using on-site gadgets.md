# 18. Bypassing SameSite restrictions using on-site gadgets

### 🚫 What Does `SameSite=Strict` Do?

- Cookies with the `SameSite=Strict` attribute **will NOT be sent in any cross-site requests**.
- This means the browser blocks cookies if the request **originates from a different site**.

---

### 🔍 But... There’s a Sneaky Bypass!

You **may be able to bypass this limitation** by leveraging a **client-side redirect gadget** — a redirect on the victim's browser controlled by attacker input, such as URL parameters.

---

### 💡 How Does It Work?

1. **Client-Side Redirects**
    - The redirect URL is dynamically constructed using attacker-controlled input (like query parameters).
    - Example: A vulnerable page that runs JavaScript like
        
        ```jsx
        window.location = location.searchParams.get('targetUrl');
        ```
        
2. **Why This Matters**
    - Browsers treat client-side redirects **not as traditional redirects** but as **new, independent same-site requests**.
    - These **same-site requests include all cookies**, even those restricted by `SameSite=Strict`.
3. **Result**
    - The attacker triggers a **secondary request within the same site**, sending cookies that would otherwise be blocked.
    - This enables **full bypass** of `SameSite=Strict` cookie protections!

---

### ⚠️ Important Distinction: Server-Side Redirects

- Server-side redirects (HTTP 3xx responses) **do NOT allow this bypass**.
- Browsers track the original request's origin, and **still apply cookie restrictions** on the redirected request.

---

### 🔐 Summary

| Mechanism | Cookies Included? | Bypass Possible? |
| --- | --- | --- |
| SameSite=Strict + GET | No | No |
| Client-Side Redirect | Yes (same-site) | **Yes!** |
| Server-Side Redirect | No | No |