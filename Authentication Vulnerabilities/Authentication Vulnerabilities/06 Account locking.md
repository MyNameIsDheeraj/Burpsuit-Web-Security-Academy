# 06. Account locking

## 🔐 Account Locking & Its Limitations

Websites often try to prevent **brute-force attacks** by **locking user accounts** after a certain number of failed login attempts.

🔒 When an account is locked, the system may return a **specific error response**, which ironically can help attackers **enumerate usernames**.

---

### 🎯 What Does Account Locking Protect Against?

✅ Account locking offers **basic protection** against:

- 🎯 Targeted brute-forcing of a **specific account**

❌ However, it **fails** to prevent brute-force attacks that target **any account at random**.

---

## 🕵️ How Attackers Work Around Account Locking

Here’s how attackers can **bypass lockout protection** using a strategic approach:

1. 📋 **Establish a list** of likely valid usernames
    - Through **username enumeration**
    - Or by using **common username lists**
2. 🔑 Create a **shortlist of common passwords**
    - Example: `password123`, `welcome1`, `12345678`
    - **Important:** Number of passwords must be **less than or equal to the lockout threshold** (e.g., 3)
3. 💥 Use **Burp Intruder** or similar tools:
    - Try each password with **every username**
    - This way, you attempt **multiple logins** without triggering the lock
    - Just **one successful match** compromises an account ✅

---

## 🧨 Why Account Locking Fails Against Credential Stuffing

Credential stuffing is an advanced brute-force tactic that renders account locking **ineffective**.

### 🧾 What is Credential Stuffing?

🚨 Attackers use a **huge dictionary of known credentials** from **previous data breaches** in the format:

```
username:password

```

🧠 Because users often **reuse passwords** across multiple sites, attackers bet that:

> Some stolen credentials will work on the target site
> 

### ⚠️ Why Account Locking Doesn’t Help

🔁 **Each credential is tried only once**, so:

- ❌ Account lock isn't triggered
- ✅ Attacker can gain access to **multiple accounts in a single attack**

🎯 This makes credential stuffing a **highly effective and dangerous method**.

---

### 🧩 Summary

| 🔒 Defense | 🛡️ Protection Against | ❌ Fails Against |
| --- | --- | --- |
| Account Locking | Targeted brute-forcing | Random brute-forcing, Credential Stuffing |

---

### 💡 Tip for Developers

Use **multi-factor authentication (MFA)** and implement **rate-limiting per IP + global IP analysis** to mitigate advanced brute-force vectors like credential stuffing.

---

Let me know if you'd like this exported as a PDF or Markdown file for inclusion in your official documentation.