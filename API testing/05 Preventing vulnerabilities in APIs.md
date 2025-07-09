# 05. Preventing vulnerabilities in APIs

When designing APIs, make sure that **security is a consideration from the beginning**.

> 🧠 Proactive design helps reduce the risk of exposure and exploitation.
> 

---

### 🔒 **General Security Best Practices**

✅ **Secure your documentation**

🔐 If your API is not meant to be public, **restrict access** to its documentation.

✅ **Keep documentation up to date**

📚 Accurate docs ensure **legitimate testers** have full visibility of the **API's attack surface**.

✅ **Apply an allowlist of HTTP methods**

📋 Explicitly define which methods (`GET`, `POST`, `PATCH`, etc.) are **permitted**.

✅ **Validate content types**

🧾 Ensure that every request/response has the **expected Content-Type**, such as `application/json`.

✅ **Use generic error messages**

❌ Avoid exposing stack traces or technical details that could help attackers.

✅ **Protect all versions of your API**

📦 Apply security controls to **all versions**, including:

- 🧪 Development
- 🧬 Staging
- 🚀 Production

---

### 🚫 **Preventing Mass Assignment Vulnerabilities**

To prevent mass assignment issues:

✅ **Allowlist** the properties that **can be updated** by the user

❌ **Blocklist** sensitive properties that **must not be updated**

> 🛡️ This ensures that users can’t tamper with internal fields like isAdmin, role, or id.
>