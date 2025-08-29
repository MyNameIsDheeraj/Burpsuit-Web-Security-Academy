# 06. Symmetric vs asymmetric algorithms

JWTs can be signed using a range of different algorithms.

These fall into **two main categories**: **symmetric** and **asymmetric**.

---

## 🔑 Symmetric Algorithms (HS256, etc.)

👉 Example: **HS256 (HMAC + SHA-256)**

- The server uses a **single secret key** to **both sign and verify** the JWT.
- This **secret must always be protected**, just like a password.
- If an attacker obtains this key, they can both **forge tokens** and **validate them**.

🖼️ Symmetric Signing Process:

![Symmetric JWT](https://portswigger.net/web-security/jwt/images/jwt-symmetric-signing-algorithm.jpg)

---

## 🧾 Asymmetric Algorithms (RS256, etc.)

👉 Example: **RS256 (RSA + SHA-256)**

- Uses an **asymmetric key pair**:
    - **Private Key** → kept secret by the server, used to **sign** tokens.
    - **Public Key** → shared openly, used to **verify** tokens.
- The **mathematical relationship** between the keys ensures that:
    - Only the server can **generate valid signatures**.
    - Anyone with the public key can **verify the authenticity** of a token.

🖼️ Asymmetric Signing Process:

![Asymmetric JWT](https://portswigger.net/web-security/jwt/images/jwt-asymmetric-signing-algorithm.jpg)

---

## ⚖️ Quick Comparison

| Feature | Symmetric (HS256) 🔑 | Asymmetric (RS256) 🧾 |
| --- | --- | --- |
| **Keys Used** | One key (shared secret) | Key pair (private + public) |
| **Signing** | Secret key | Private key |
| **Verification** | Same secret key | Public key |
| **Key Sharing** | Must stay secret | Public key can be distributed |
| **Risk** | If key leaks → full compromise | Safer (public key disclosure is fine) |