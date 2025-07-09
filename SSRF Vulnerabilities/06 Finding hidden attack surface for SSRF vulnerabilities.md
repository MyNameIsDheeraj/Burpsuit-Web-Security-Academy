# 06. Finding hidden attack surface for SSRF vulnerabilities

Many **Server-Side Request Forgery (SSRF)** vulnerabilities are easy to identify, especially when request parameters contain full URLs. However, **some SSRF flaws are more subtle** and require deeper inspection.

---

### 🔍 Partial URLs in Requests

🧩 Sometimes, an application places **only a hostname** or **a partial path** into request parameters. The server-side then builds a **full URL** using this value.

🟠 These are still SSRF attack surfaces, but:

- You might not control the **entire requested URL**
- The SSRF **exploitability might be limited**

> 🧠 Be alert to hostnames or URL fragments in parameters — these could be stitched into sensitive internal requests server-side.
> 

---

### 📦 URLs Within Data Formats

Some apps transmit data using formats that **allow embedded URLs**, which may be processed by the **server's data parsers**.

⚠️ One common format is **XML**, which:

- Supports **external entities**
- Can trigger **SSRF via XXE injection**

> We'll explore this further in the XXE injection section, but remember: SSRF via XML is real and often overlooked.
> 

---

### 📡 SSRF via the Referer Header

🧪 Some apps use server-side analytics tools to **track visitor behavior** by logging the `Referer` header.

📉 These tools often:

- Analyze **third-party URLs** in the header
- Visit the links to gather data like anchor text

🧨 As a result, this makes the `Referer` header a **valuable SSRF attack vector**.

> 🎯 Tip: Inject malicious URLs into the Referer header — if visited server-side, you've uncovered SSRF!
> 

---

### 🛠️ Summary

| Vector | Description | SSRF Risk |
| --- | --- | --- |
| 🔹 Partial URLs in Parameters | Hostname or path only; URL is completed on the server | Medium |
| 🔸 URLs in XML/Structured Data | SSRF triggered by parsers like XML parsers (XXE) | High |
| 🔺 Referer Header | Analytics tools may visit URLs in Referer headers | Medium |