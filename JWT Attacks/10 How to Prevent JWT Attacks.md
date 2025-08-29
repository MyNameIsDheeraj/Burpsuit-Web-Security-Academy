# 10. How to Prevent JWT Attacks

You can protect your own websites against many of the attacks we’ve covered by following these **high-level security measures**:

---

## ✅ Core Security Measures

1. 📚 **Use an up-to-date JWT library**
    - Ensure developers fully understand how it works and its security implications.
    - Modern libraries reduce insecure implementations but ⚠️ aren’t foolproof due to JWT’s flexibility.
2. 🔏 **Perform robust signature verification**
    - Verify signatures of **all JWTs you receive**.
    - Account for **edge cases** (e.g., unexpected algorithms).
3. 🌐 **Enforce a strict whitelist for the `jku` header**
    - Only allow trusted hosts.
4. 🚫 **Prevent injection attacks via the `kid` header**
    - Ensure you’re not vulnerable to **path traversal** or **SQL injection**.

---

## 📋 Additional Best Practices for JWT Handling

Although not strictly required to prevent vulnerabilities, following these practices will make your application **much safer**:

1. ⏳ **Always set an expiration date (`exp`)**
    - Prevents indefinite token reuse.
2. 🚫 **Avoid sending tokens in URL parameters**
    - Prefer using **HTTP headers** (e.g., `Authorization: Bearer <token>`).
3. 🎯 **Include the `aud` (audience) claim**
    - Specifies the **intended recipient** of the token.
    - Stops the token from being reused on different sites.
4. 🔄 **Enable token revocation**
    - Let the server revoke tokens (e.g., during logout).

---

# 🔐 Summary

By combining **robust verification**, **safe header handling**, and **best practices** like expiration and revocation, you can significantly reduce the risk of **JWT-based attacks** in your applications.