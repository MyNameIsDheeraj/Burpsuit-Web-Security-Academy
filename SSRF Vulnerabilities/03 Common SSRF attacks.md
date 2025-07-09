# 03. Common SSRF attacks

## 🎯 SSRF Attacks: Exploiting Trust Relationships

---

### 🧨 Introduction

**Server-Side Request Forgery (SSRF)** attacks often exploit **trust relationships** to escalate from a seemingly harmless interaction to **unauthorized access or actions**.

These trust relationships might exist:

- 🔁 On the **server itself**
- 🖧 Across **other internal systems** within the same organization

---

## 🛠️ SSRF Attacks Against the Server

In this scenario, the attacker causes the **application to make a request back to itself** via the **loopback interface**, using:

- 🧩 `127.0.0.1` (loopback IP)
- 🧩 `localhost` (loopback domain)

---

### 🛍️ Example: Stock Check SSRF

Imagine a shopping site lets users check stock levels. It does so by making an internal request via a user-supplied API:

```
POST /product/stock HTTP/1.0
Content-Type: application/x-www-form-urlencoded
Content-Length: 118

stockApi=http://stock.weliketoshop.net:8080/product/stock/check%3FproductId%3D6%26storeId%3D1
```

🔁 The server fetches the URL and displays the result to the user.

---

### 🔓 Exploiting the Server’s Trust

An attacker modifies the request:

```
POST /product/stock HTTP/1.0
Content-Type: application/x-www-form-urlencoded
Content-Length: 118

stockApi=http://localhost/admin
```

📥 The server fetches `/admin` — normally restricted to authenticated users.

❗ **But now**, because the request comes from `localhost`, the application may **bypass access controls** and expose **admin functionality**.

---

### ❓ Why Do Applications Trust Local Requests?

This behavior can occur due to several reasons:

- 🛡️ Access controls enforced by a **reverse proxy** in front of the app
- 🔁 **Disaster recovery** fallback: Admin access granted locally in case credentials are lost
- 📦 Admin interface on a **different port** or bound only to `127.0.0.1`

> ⚠️ These assumptions often lead to critical vulnerabilities when SSRF is possible.
> 

---

## 🧱 SSRF Attacks Against Other Back-End Systems

Sometimes, the application can access **internal services** (e.g., databases, internal APIs) on **private IPs**, like `192.168.x.x` or `10.x.x.x`.

These are **not directly accessible** by users and often:

- 🔓 Lack proper authentication
- 📉 Have a weak security posture

---

### 🌐 Exploiting Internal Systems

If an admin interface exists at `http://192.168.0.68/admin`, an attacker can send:

```
POST /product/stock HTTP/1.0
Content-Type: application/x-www-form-urlencoded
Content-Length: 118

stockApi=http://192.168.0.68/admin
```

✅ The server **makes the request internally** and may return restricted admin content.

---

### 🧠 Key Insight

> SSRF transforms a client-controlled request into a server-executed attack, bypassing protections and reaching otherwise unreachable systems.
>