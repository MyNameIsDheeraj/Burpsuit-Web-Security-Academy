# 05. Brute-forcing secret keys

Some signing algorithms, such as **HS256** (HMAC + SHA-256) 🛡, use an **arbitrary standalone string** as the **secret key** 🔑.

Just like a password, this secret **must not** be easily guessed or brute-forced.

⚠️ **Why?**

If an attacker guesses or cracks the secret:

- They can create JWTs with **any header and payload** they want
- Then **re-sign the token** with a valid signature 🕵️‍♂️

---

## 🛠 Common Developer Mistakes

❌ Forgetting to change **default/placeholder secrets**

❌ Copy-pasting **example code** from the internet and keeping the **hardcoded secret**

💡 These mistakes make it **trivial** for an attacker to brute-force the server’s secret using a **wordlist of well-known keys** 📜.

---

## ⚡ Brute-Forcing with Hashcat

We recommend using [**hashcat**](https://hashcat.net/wiki/doku.php?id=frequently_asked_questions#how_do_i_install_hashcat) 🐱‍💻 to brute-force JWT secret keys.

✅ Hashcat is pre-installed on **Kali Linux** (bare metal installer version).

⚠️ **Note:** The **pre-built VirtualBox image** for Kali may not have enough **memory** to run hashcat.

---

## 📦 Requirements

You need:

- A **valid, signed JWT** from the target server 🪪
- A [**wordlist**](https://github.com/wallarm/jwt-secrets/blob/master/jwt.secrets.list) of well-known secrets 📄

---

## 💻 Command to Run

```bash
hashcat -a 0 -m 16500 <jwt> <wordlist>
```

🔍 **How it works:**

- Hashcat signs the **header + payload** from the JWT with each secret in the wordlist
- Compares the generated signature with the original one from the server
- If a match is found, hashcat outputs:

```
<jwt>:<identified-secret>
```

---

## 📝 Notes

- If you run the command more than once, include:

```
--show
```

to display results.

- Hashcat runs **locally** 🖥 and does **not send requests** to the server making it **extremely fast**, even with huge wordlists 🚀.

---

## 🔓 Once You Have the Secret

With the **identified secret key**, you can:

- Generate a **valid signature** for any JWT header and payload you want ✏️
- Re-sign modified JWTs (see *Editing JWTs in Burp Suite*)

💡 If the server uses an **extremely weak secret**, you might even brute-force it **character-by-character** without a wordlist.