# 01. What are JSON web tokens (JWTs)?

In this section, we'll explore how **design flaws** and **improper handling** of **JSON Web Tokens (JWTs)** can make websites vulnerable to **high-severity attacks**.

Since JWTs are widely used in **authentication**, **session management**, and **access control**, exploiting them can potentially **compromise an entire website and its users**.

💡 Don’t worry if you’re new to JWTs — we’ll explain everything step-by-step, with **vulnerable labs** for safe, hands-on practice.

![image.png](Img/imagemain.png)

---

## 📦 **What are JWTs?**

**JSON Web Tokens (JWTs)** are a **standardized format** for sending **cryptographically signed JSON data** between systems.

- Can contain **any kind of data**
- Most commonly used to send **"claims"** about users
- Common in **authentication**, **session handling**, **access control**

🔹 Unlike classic session tokens:

- All the data the server needs is stored **client-side** in the JWT itself
- Popular for **distributed systems** where users interact with **multiple backend servers** seamlessly

---

## 🧩 **JWT Structure**

A JWT has **3 parts**, separated by dots (`.`):

```
header.payload.signature
```

Example:

```json
eyJraWQiOiI5MTM2ZGRiMy1jYjBhLTRhMTktYTA3ZS1lYWRmNWE0NGM4YjUiLCJhbGciOiJSUzI1NiJ9.eyJpc3MiOiJwb3J0c3dpZ2dlciIsImV4cCI6MTY0ODAzNzE2NCwibmFtZSI6IkNhcmxvcyBNb250b3lhIiwic3ViIjoiY2FybG9zIiwicm9sZSI6ImJsb2dfYXV0aG9yIiwiZW1haWwiOiJjYXJsb3NAY2FybG9zLW1vbnRveWEubmV0IiwiaWF0IjoxNTE2MjM5MDIyfQ.SYZBPIBg2CRjXAJ8vCER0LA_ENjII1JakvNQoP-Hw6GG1zfl4JyngsZReIfqRvIAEi5L4HV0q7_9qGhQZvy9ZdxEJbwTxRs_6Lb-fZTDpW6lKYNdMyjw45_alSCZ1fypsMWz_2mTpQzil0lOtps5Ei_z7mM7M8gCwe_AGpI53JxduQOaB5HkT5gVrv9cKu9CsW5MS6ZbqYXpGyOG5ehoxqm8DL5tFYaW3lB50ELxi0KsuTKEbD0t5BCl0aCR2MBJWAbN-xeLwEenaqBiwPVvKixYleeDQiBEIylFdNNIMviKRgXiYuAvMziVPbwSgkZVHeEdF5MQP1Oe2Spac-6IfA
```

---

### 📜 **Header**

- Contains **metadata** about the token (algorithm, type, etc.)

### 🧾 **Payload**

- Contains **claims** about the user
    
    Example (decoded from above token):
    

```json
{
    "iss": "portswigger",
    "exp": 1648037164,
    "name": "Carlos Montoya",
    "sub": "carlos",
    "role": "blog_author",
    "email": "carlos@carlos-montoya.net",
    "iat": 1516239022
}

```

⚠️ Anyone with the token can **read or modify** header & payload — **security depends entirely on the signature**.

---

## ✍️ **JWT Signature**

The server generates the **signature** by:

1. Hashing the **header + payload**
2. Using a **secret signing key**
3. Sometimes encrypting the hash

🔹 Signature ensures **data integrity**:

- Changing **1 byte** in header/payload → signature mismatch
- Without the **secret key**, attackers **should not** be able to forge a valid signature

💡 **Pro tip:**

Use [jwt.io](https://jwt.io/) to **decode & debug** tokens for better understanding.

---

## 🔄 **JWT vs JWS vs JWE**

📜 **JWT spec**: Defines only the **format** for claims as JSON.

- **JWS (JSON Web Signature)**: JWT + Signature
- **JWE (JSON Web Encryption)**: JWT + Encryption of contents

![image.png](Img/image_1.png)

💡 In practice:

- "JWT" usually means **JWS token**
- **JWE** is similar but keeps contents **encrypted**, not just encoded