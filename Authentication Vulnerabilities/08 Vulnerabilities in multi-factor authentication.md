# 08. Vulnerabilities in multi-factor authentication

In this section, we'll look at some of the **vulnerabilities** that can occur in **multi-factor authentication mechanisms**.

🧪 Several **interactive labs** are available to demonstrate how you can exploit these vulnerabilities in MFA.

---

## 🔑 Why Use MFA?

Many websites rely exclusively on **single-factor authentication** using a password.

However, more secure systems require users to prove their identity using **multiple authentication factors**:

### 👇 Common MFA Factors

- 🧠 **Something you know** (e.g. password)
- 📱 **Something you have** (e.g. phone, token)
- 🧬 **Something you are** (e.g. fingerprint)

> ✅ MFA increases security, but only if implemented correctly.
> 

---

## ⚠️ Implementation Weaknesses

While it's difficult for an attacker to obtain **both factors** at the same time, **poor implementation** can allow them to:

- 🎯 Bypass MFA entirely
- 📥 Intercept verification codes
- 🚫 Exploit the same factor verified twice

---

## 🛑 Not All MFA is True MFA

🔍 Verifying the same factor twice ≠ **true two-factor authentication**.

### 📧 Example: Email-based "2FA"

- ✅ User enters password
- 🔄 Code is sent to email
- 📌 But email is protected by… the same password!

> 🧠 You're just verifying knowledge twice — not adding a new factor.
> 

---

## 📟 Two-Factor Authentication Tokens

### 🔒 Secure MFA Devices:

- 🔐 RSA token devices
- ⌨️ Keypad tokens (often used by banks)
- 📲 Mobile apps (e.g. Google Authenticator, Authy)

These generate the code **on-device**, making them harder to intercept.

### 📵 SMS-based MFA: The Weak Link

Some websites send codes via **SMS**:

- 🚧 SMS is easier to intercept
- 🧬 Vulnerable to **SIM swapping**
    - Attacker gains control of victim’s number
    - Receives all SMS codes, including MFA tokens

---

## 🚨 Bypassing MFA

Sometimes the **MFA process** itself is flawed.

### 🧪 Example Scenario:

1. 🧍‍♂️ User enters correct **password**
2. 🔁 Then prompted for **verification code**
3. 🔓 **But**... they’re already partially authenticated!

> 🔍 Try accessing restricted pages after Step 1.
> 
> 
> If the site doesn’t validate the second step, **MFA is effectively bypassed**.
>