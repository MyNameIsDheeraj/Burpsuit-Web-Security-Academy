# 05. Blind SSRF vulnerabilities

> Blind SSRF occurs when an application makes a back-end HTTP request to a URL supplied by the attacker — but does not return the response to the attacker.
> 

It’s **harder to detect**, but may lead to serious consequences such as **Remote Code Execution (RCE)** on the server or connected systems.

---

### 💥 What is the Impact of Blind SSRF?

- ⚠️ Typically **lower** than a full SSRF (no response leakage)
- ❌ Cannot **directly retrieve data**
- 💣 Still can lead to **critical issues** like:
    - Remote Code Execution
    - Lateral network scanning
    - Detection of other back-end vulnerabilities

---

### 🔍 How to Detect and Exploit Blind SSRF

### 🛰️ Use Out-of-Band (OAST) Techniques

> This method involves sending requests to external systems you control, and watching for incoming interactions.
> 

### 🛠️ Tool: **Burp Collaborator**

- Generate unique payload domains (e.g., `abc123.oastify.com`)
- Inject them in suspected parameters
- **Monitor Collaborator** for:
    - DNS lookups
    - HTTP requests
    - Other unexpected interactions

---

### ⚠️ Note on DNS-only Lookups

🧩 You may **observe a DNS request** but **not an HTTP request** — why?

✅ Reason:

- The app tries to make an HTTP request.
- DNS resolves the domain.
- But **network-level filtering blocks HTTP**, allowing only DNS.

> ⚠️ This is common in restrictive internal environments.
> 

---

### 🚧 Exploit Challenges

- You **can’t see the HTTP response**
- You **can’t browse** or list back-end data

> However...
> 

### 🧪 You *can* still:

- **Blindly scan internal networks** (e.g., `192.168.x.x`)
- Test for **well-known vulnerabilities** using **OAST** payloads
- Detect unpatched, vulnerable services

---

### ☠️ Advanced Exploitation: Inducing RCE

Blind SSRF can be weaponized by:

1. Forcing the app to connect to a server you **fully control**
2. Returning a **malicious payload** in the HTTP response
3. Exploiting a **vulnerability in the client's HTTP parser**
4. Achieving **Remote Code Execution**

---

### 📌 Summary

| Technique | Purpose | Tool/Notes |
| --- | --- | --- |
| 🛰️ OAST | Detect blind SSRF via DNS/HTTP ping | Use Burp Collaborator |
| 🔎 DNS-only detection | Identify blocked HTTP | Still useful as SSRF indicator |
| 🧪 Internal scanning | Find internal vulnerable services | Use known exploits via SSRF |
| 🛠️ RCE via HTTP client | Advanced, risky but powerful | Craft malicious HTTP responses |