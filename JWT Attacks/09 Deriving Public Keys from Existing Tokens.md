# 09. Deriving Public Keys from Existing Tokens

In cases where the **public key isn’t readily available**, you may still be able to test for **algorithm confusion** by deriving the key from a pair of existing JWTs.

This process is relatively simple using tools such as **`jwt_forgery.py`**.

👉 You can find this, along with several other useful scripts, on the rsa_sign2n [GitHub repository](https://github.com/).

---

## 🐳 One-Command Simplified Tool (Docker)

We’ve also created a **simplified version** of this tool, which you can run with a single command:

```bash
docker run --rm -it portswigger/sig2n <token1> <token2>
```

---

## 📌 Note

- 🐋 You need the **Docker CLI** to run either version of the tool.
- ⏳ The first time you run this command, it will **pull the image from Docker Hub**, which may take a few minutes.

---

## ⚙️ What the Tool Does

The script uses the **JWTs you provide** to calculate one or more potential values of `n`.

👉 Don’t worry too much about the math behind it — all you need to know is:

- ✅ Only **one** of these values will match the `n` used by the server’s key.

For each potential value, the script outputs:

- 📄 A **Base64-encoded PEM key** in both **X.509** and **PKCS1** format.
- 🔑 A **forged JWT** signed using each of these keys.

---

## 🔍 Identifying the Correct Key

1. Use **Burp Repeater** to send a request containing each forged JWT.
2. Only **one of them will be accepted** by the server.
3. ✅ Once identified, use the **matching key** to construct an **algorithm confusion attack**.

---

## 📚 Learn More

For detailed info:

- 📖 Check out the documentation in the **rsa_sign2n repository**.
- 🔐 For more labs, explore the rest of our topic on [**JWT Attacks**](https://portswigger.net/web-security/jwt).