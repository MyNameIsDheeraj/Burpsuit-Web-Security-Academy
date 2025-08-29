# 02. What are JWT attacks?

JWT attacks involve a user sending **modified JWTs** to the server in order to achieve a **malicious goal**.

Typically, this goal is to **bypass authentication** and **access controls** by **impersonating another user** who has already been authenticated.

## ⚠️ **What is the impact of JWT attacks?**

The impact of JWT attacks is usually **severe**.

If an attacker is able to **create their own valid tokens** with arbitrary values, they may be able to:

- Escalate their own privileges
- Impersonate other users
- Take **full control** of their accounts

## 🛠 **How do vulnerabilities to JWT attacks arise?**

JWT vulnerabilities typically arise due to **flawed JWT handling** within the application itself.

The JWT specifications are **flexible by design**, allowing developers to decide many implementation details themselves.

This flexibility can lead to **accidental vulnerabilities** even when using **secure libraries**.

Common issues include:

- The **JWT signature is not verified** properly, enabling attackers to tamper with payload values.
- Even if the signature is verified, **trust depends on the secrecy** of the server's secret key.
- If the secret key is **leaked**, **guessed**, or **brute-forced**, attackers can generate **valid signatures** for any token, effectively compromising the entire system.

### 💡 **Key takeaway:**

Keep your JWT handling **secure**, always **verify signatures**, and **protect your secret keys** like your application depends on it because it does.