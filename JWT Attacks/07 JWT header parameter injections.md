# 07. JWT header parameter injections

According to the **JWS specification**, only the `alg` header parameter is mandatory.

In practice, however, JWT headers (**JOSE headers**) often contain several other parameters.

⚠️ The following ones are of particular interest to attackers:

- 🔐 **jwk (JSON Web Key)** – Provides an embedded JSON object representing the key.
- 🌍 **jku (JSON Web Key Set URL)** – Provides a URL from which servers can fetch a set of keys containing the correct key.
- 🆔 **kid (Key ID)** – Provides an ID that servers can use to identify the correct key when multiple keys exist.

👉 These **user-controllable parameters** each tell the recipient server **which key to use** when verifying the signature.

If misused, attackers can inject modified JWTs signed with their **own arbitrary key** instead of the server’s secret.

---

## 🔐 Injecting Self-Signed JWTs via the `jwk` Parameter

📜 The **JWS specification** describes an optional `jwk` header parameter.

Servers can use it to **embed their public key directly** within the token itself in **JWK format**.

### 🧩 What is a JWK?

A **JWK (JSON Web Key)** is a standardized format for representing keys as a JSON object.

✅ Example JWT header with `jwk`:

```json
{
    "kid": "ed2Nf8sb-sD6ng0-scs5390g-fFD8sfxG",
    "typ": "JWT",
    "alg": "RS256",
    "jwk": {
        "kty": "RSA",
        "e": "AQAB",
        "kid": "ed2Nf8sb-sD6ng0-scs5390g-fFD8sfxG",
        "n": "yy1wpYmffgXBxhAUJzHHocCuJolwDqql75ZWuCQ_cb33K2vh9m"
    }
}

```

🔑 **Public vs Private Keys**

- **Public Key** – Shared, used to verify signatures.
- **Private Key** – Secret, used to create signatures.

⚠️ Ideally, servers should only use **whitelisted public keys**.

But some misconfigured servers accept **any key in the jwk parameter**.

👉 Exploit:

1. Sign a JWT using **your own RSA private key**.
2. Embed the matching **public key in the `jwk` header**.

🛠️ Using **Burp JWT Editor Extension**:

- Generate a new RSA key.
- Modify the token payload.
- Use **Attack → Embedded JWK** to test if the server accepts it.

---

## 🌍 Injecting Self-Signed JWTs via the `jku` Parameter

Instead of embedding keys via `jwk`, some servers allow a **`jku` (JWK Set URL)** header parameter.

👉 This points to a **JWK Set** containing the key.

### 🧩 What is a JWK Set?

A **JWK Set** is a JSON object containing an array of keys.

✅ Example JWK Set:

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

💡 Many websites expose JWK Sets publicly at:

```
/.well-known/jwks.json

```

⚠️ Secure servers fetch keys only from **trusted domains**.

But attackers may exploit **URL parsing discrepancies (SSRF)** to bypass filters.

---

## 🆔 Injecting Self-Signed JWTs via the `kid` Parameter

The `kid` (Key ID) parameter tells the server **which key to use**.

📂 Verification keys are often stored in a **JWK Set**.

The server may simply look for the `kid` matching the token.

👉 But the `kid` is **just an arbitrary string** chosen by the developer.

It could reference:

- A **database entry**
- A **file path**

✅ Example malicious JWT header:

```json
{
    "kid": "../../path/to/file",
    "typ": "JWT",
    "alg": "HS256",
    "k": "asGsADas3421-dfh9DGN-AFDFDbasfd8-anfjkvc"
}

```

### ⚠️ Exploit Scenarios

- 🗂️ **Directory Traversal** → Force server to use arbitrary file as verification key.
- 🔄 **Symmetric Algorithm Misuse** → Point `kid` to a predictable file (e.g., `/dev/null`).
    - `/dev/null` returns an empty string.
    - Signing JWT with an **empty string** = valid signature.
- 💉 **SQL Injection** → If `kid` is used in database lookups.

---

## 🧩 Other Interesting JWT Header Parameters

- 📦 **cty (Content Type)** – Declares payload type.
    - Possible attack: Change content type to `text/xml` or `application/x-java-serialized-object`.
    - Enables **XXE or deserialization attacks** if signature verification is bypassed.
- 📜 **x5c (X.509 Certificate Chain)** – Embeds certificate chains.
    - Attack: Inject **self-signed certificates**, similar to `jwk` injection.
    - ⚠️ X.509 parsing can introduce vulnerabilities.
    - See: **CVE-2017-2800** & **CVE-2018-2633**.

---

## 🛡️ Key Takeaways

- 🔑 JWT headers contain **dangerous, user-controllable parameters**.
- ⚡ Misconfigurations allow **self-signed JWTs** to be trusted.
- 🚨 Exploits possible via:
    - `jwk` → Embed public key.
    - `jku` → Host malicious JWK Set.
    - `kid` → Path traversal / SQLi / empty string trick.
- 🧨 Other params like `cty` and `x5c` can expand the attack surface.