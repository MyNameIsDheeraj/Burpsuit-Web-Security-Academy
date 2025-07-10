# 10. Brute-Forcing 2FA Verification Codes

> As with passwords, websites need to take steps to prevent brute-forcing of the 2FA verification code.
> 
> 
> This is especially important because the code is often a simple **4 or 6-digit number**. Without adequate brute-force protection, cracking such a code is **trivial**.
> 

---

### 🚫 Ineffective Protections

Some websites attempt to prevent brute-forcing by:

🛑 **Automatically logging a user out**

➡️ after they enter a certain number of incorrect verification codes.

❌ However, this method is **ineffective in practice**.

---

### 🤖 Advanced Automation Techniques

An advanced attacker can **automate** the multi-step brute-force process using tools such as:

- 🧩 **Burp Intruder Macros** — to automate complex request sequences.
- ⚡ **Turbo Intruder extension** — built specifically for high-speed request generation.

---

### 🔁 Why This Matters

📉 Without proper rate-limiting or lockout mechanisms, attackers can easily:

- Iterate through all **10000 combinations** (0000–9999) for 4-digit codes.
- Perform **brute-force attacks** at scale using automation tools.

---

> 🔒 Mitigation Tip: Always implement proper rate limiting, session tracking, and account lockout mechanisms for 2FA steps.
>