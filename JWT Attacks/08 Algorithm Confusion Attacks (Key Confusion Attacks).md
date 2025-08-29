# 08. Algorithm Confusion Attacks (Key Confusion Attacks)

**Algorithm confusion attacks** (also known as **key confusion attacks**) occur when an attacker forces the server to verify the signature of a **JSON Web Token (JWT)** using a different algorithm than the developers intended.

⚠️ If this case isn’t handled properly, attackers can **forge valid JWTs** with arbitrary values **without knowing the server’s secret signing key**.

---

## 🐞 Why Algorithm Confusion Happens

- These vulnerabilities typically arise due to **flawed JWT library implementations**.
- Many libraries provide a **generic `verify()` method**, which relies on the **`alg` parameter** in the JWT header to decide which verification method to use.

### 🧑‍💻 Example: Pseudo-code of a vulnerable `verify()` function

```jsx
function verify(token, secretOrPublicKey){
    algorithm = token.getAlgHeader();
    if(algorithm == "RS256"){
        // Use the provided key as an RSA public key
    } else if (algorithm == "HS256"){
        // Use the provided key as an HMAC secret key
    }
}
```

👉 The problem: Developers often assume the server **only uses asymmetric algorithms (like RS256)** and always pass a **fixed public key**.

```jsx
publicKey = <public-key-of-server>;
token = request.getCookie("session");
verify(token, publicKey);

```

💥 If an attacker sets `alg: HS256`, the library treats the **public key as an HMAC secret**.

➡️ The attacker can then sign the JWT using **HS256** with the **public key** and trick the server.

---

## 📌 Important Note

🔑 The **public key used to sign** the token must be **identical** to the one stored on the server:

- ✅ Same format (e.g., **X.509 PEM**)
- ✅ Includes all non-printing characters (like newlines)

> 🧪 In practice, you may need to experiment with formatting for the attack to succeed.
> 

---

## 🚀 Performing an Algorithm Confusion Attack

Here’s the **step-by-step process** to exploit this vulnerability 👇

---

### 🔎 Step 1 - Obtain the Server’s Public Key

- Servers may expose their **public keys** via endpoints such as:
    
    ```
    /jwks.json
    /.well-known/jwks.json
    ```
    
- These are stored as **JSON Web Key Sets (JWKS)**.

📄 Example JWK response:

```json
{
    "keys": [
        {
            "kty": "RSA",
            "e": "AQAB",
            "kid": "75d0ef47-af89-47a9-9061-7c02a610d5ab",
            "n": "o-yy1wpYmffgXBxhAUJzHHocCuJolwDqql75ZWuCQ_cb33K2vh9mk6GPM9gNN4Y_qTVX67WhsN3JvaFYw-fhvsWQ"
        },
        {
            "kty": "RSA",
            "e": "AQAB",
            "kid": "d8fDFo-fS9-faS14a9-ASf99sa-7c1Ad5abA",
            "n": "fc3f-yy1wpYmffgXBxhAUJzHql79gNNQ_cb33HocCuJolwDqmk6GPM4Y_qTVX67WhsN3JvaFYw-dfg6DH-asAScw"
        }
    ]
}
```

👉 Even if the key isn’t public, you may extract it from a **pair of existing JWTs**.

---

### 🔄 Step 2 - Convert the Public Key to a Suitable Format

- The server may store its local copy in a **different format** (e.g., PEM).
- You must use a version that is **byte-for-byte identical**.

🔧 Convert JWK → PEM in **Burp Suite (JWT Editor extension):**

1. Load the **JWT Editor** extension.
2. Go to **JWT Editor → Keys tab** → Click **New RSA Key**.
3. Paste the **JWK** obtained earlier.
4. Select **PEM format** → Copy the resulting PEM key.
5. In **Decoder**, Base64-encode the PEM.
6. Back in **JWT Editor Keys tab**, click **New Symmetric Key**.
7. Replace the `k` value with the **Base64-encoded PEM key**.
8. ✅ Save the key.

---

### 📝 Step 3 - Modify the JWT

- Change the **header** to:
    
    ```json
    { "alg": "HS256" }
    ```
    
- Modify the **payload** with arbitrary values (e.g., make yourself admin).

---

### ✍️ Step 4 - Sign the JWT

- Sign the token using:
    - Algorithm: **HS256**
    - Secret: **RSA Public Key (in correct format)**

---

## 🎉 Final Result

The server will **treat the public key as the HMAC secret**, accept your forged JWT, and grant **unauthorized access** 🚀.