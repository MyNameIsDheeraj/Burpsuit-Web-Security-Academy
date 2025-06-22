# 24. What is client-side template injection?

### 🛠️ What Are They?

Client-side template injection vulnerabilities arise when applications using a **client-side template framework** dynamically embed **user input** in web pages.

---

### 🔍 How It Works

When rendering a page, the framework:

- Scans the page for **template expressions**
- Executes any template expressions it encounters

---

### 🚨 Attack Vector

An attacker can exploit this behavior by supplying a **malicious template expression** that launches a **cross-site scripting (XSS) attack**.