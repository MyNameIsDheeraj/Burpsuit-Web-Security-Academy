# 12. Preventing server-side parameter pollution

### ✅ Best Practices

To protect your application from **server-side parameter pollution**, follow these practices:

---

### 1️⃣ 🧾 Use an **Allowlist**

Define which characters are considered safe and **don’t require encoding**.

- 🛑 All other characters should be **properly encoded**.
- ✅ This prevents attackers from injecting unexpected parameters.

---

### 2️⃣ 🔐 Encode All User Input

Ensure that **all user-supplied input** is:

- Properly **encoded** before being included in any **server-side request**
- Validated against the **expected character set**

---

### 3️⃣ 🔎 Enforce Strict Format Validation

Make sure that all input:

- Adheres to the **expected format** (e.g., string, integer, JSON)
- Matches the **expected structure** before being processed

> ⚠️ Never trust user input—even if it looks harmless. Validate and encode everything.
>