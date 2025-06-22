# Lab 16:Reflected XSS protected by CSP, with CSP bypass

This lab demonstrates how **Content Security Policy (CSP)** can be manipulated when a reflected XSS vulnerability exists and certain CSP directives are under attacker control.

---

## 🎯 Goal

> Perform a cross-site scripting attack that bypasses CSP and calls the alert function.
> 

> ⚠️ The intended solution works only in Google Chrome.
> 

---

## 🧪 Steps to Solve

### 1. 🧑‍💻 Inject a Classic XSS Payload

Enter this into the search box:

```html
<img src=1 onerror=alert(1)>
```

> ✅ You'll observe the payload is reflected, but CSP blocks script execution.
> 

---

### 2. 🕵️ Analyze the Response

- Use **Burp Suite's Proxy** tool to intercept the request.
- Notice the response contains a `Content-Security-Policy` header.
- The header includes a directive like:
    
    ```
    report-uri /some/path?token=...
    ```
    

🧩 **Key Insight**: You **control** the `token` parameter!

That means you can **inject your own CSP directives**.

---

### 3. 💥 Bypass CSP

Visit this crafted URL (replace `YOUR-LAB-ID` with your lab instance ID):

```
https://YOUR-LAB-ID.web-security-academy.net/?search=%3Cscript%3Ealert%281%29%3C%2Fscript%3E&token=;script-src-elem%20%27unsafe-inline%27
```

---

## 🔍 How the Exploit Works

| 🧩 Technique | 💬 Explanation |
| --- | --- |
| `token=;script-src-elem 'unsafe-inline'` | Ends current CSP directive and **injects a new one** |
| `script-src-elem` | Targets **inline `<script>` elements** |
| `'unsafe-inline'` | **Allows inline JavaScript** like `<script>alert(1)</script>` |
| `%3Cscript%3Ealert(1)%3C/script%3E` | URL-encoded inline JavaScript payload |

---

## ▶️ Community Walkthrough

📺 [Watch Solution Video](https://youtu.be/hx9DjDxuYOE)