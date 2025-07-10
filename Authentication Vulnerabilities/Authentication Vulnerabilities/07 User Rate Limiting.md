# 07. User Rate Limiting

Websites often implement **user rate limiting** to defend against brute-force attacks. Here's how it works:

📌 If too many login requests are made in a short span of time, the **user’s IP address** gets blocked.

### 🔓 IP Unblocking Methods

Blocked IPs can typically be unblocked in one of the following ways:

- ⏳ **Automatically** after a certain period has elapsed
- 👨‍💼 **Manually by an administrator**
- 🧠 **Manually by the user** after completing a CAPTCHA

---

### ✅ Pros and ❗ Cons

✔️ **Preferred over account locking**

User rate limiting is generally **less vulnerable** to:

- Username enumeration
- Denial-of-service attacks

⚠️ **Still Bypassable**

An attacker can:

- 🚀 **Spoof IP addresses**
- 🧪 **Manipulate requests** to guess multiple passwords per request

---

## 🔐 HTTP Basic Authentication

Although an **older** method, HTTP Basic Authentication is still occasionally used due to its **simplicity**.

### 🔧 How It Works

The server sends an **authentication token**, which the browser stores. This token is:

📦 `username:password` → Encoded in **Base64**

📥 Sent in every request header as:

```
Authorization: Basic base64(username:password)
```

---

### ❌ Security Risks

🚨 **Insecure Transmission**

- If **HSTS** isn't implemented, credentials are exposed to **man-in-the-middle attacks**.

🚨 **Brute-force Risk**

- Tokens are **static**, and most implementations **lack brute-force protection**.

🚨 **Session Exploits**

- HTTP Basic Authentication is **especially vulnerable to CSRF** attacks.
- It offers **no session handling**, leaving doors open for exploits.

🔑 **Even "uninteresting" pages** accessed this way can leak **reused credentials** that are valid elsewhere.