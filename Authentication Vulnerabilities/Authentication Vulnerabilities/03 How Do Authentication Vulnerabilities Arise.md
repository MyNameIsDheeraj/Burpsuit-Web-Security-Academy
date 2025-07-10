# 03. How Do Authentication Vulnerabilities Arise?

Authentication vulnerabilities are critical weaknesses that **undermine user identity verification** and allow attackers to gain unauthorized access.

---

### 🔓 Common Causes of Authentication Vulnerabilities

🛡️ **1. Weak Authentication Mechanisms**

> The authentication mechanisms are weak because they fail to adequately protect against brute-force attacks.
> 

Examples include:

- No rate limiting on login attempts
- Use of predictable usernames or passwords
- Inadequate password policies

---

🧠 **2. Broken Authentication (Logic Flaws)**

> Logic flaws or poor coding in the implementation allow the authentication mechanisms to be bypassed entirely by an attacker. This is sometimes called "broken authentication".
> 

Examples include:

- Flawed session handling
- Trusting client-side input for access control
- Improper implementation of multi-factor authentication

---

### ⚠️ Why These Flaws Matter

In many areas of web development, logic flaws might just cause the website to behave unexpectedly.

But when it comes to **authentication**, even small flaws:

- Can become **critical security issues**
- May allow **unauthorized access**
- Risk **compromise of user accounts** and **sensitive data**