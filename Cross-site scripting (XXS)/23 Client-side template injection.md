# 23. Client-side template injection

### 📚 Overview

In this section, we'll look at **client-side template injection vulnerabilities** and how you can exploit them for **XSS attacks**.

This attack technique was pioneered by our research team — read more in

👉 [XSS without HTML: Client-Side Template Injection with AngularJS](https://portswigger.net/research/xss-without-html-client-side-template-injection-with-angularjs).

---

### ⚙️ Focus on AngularJS

Although **client-side template injection** is a generic issue, we'll focus on examples from the **AngularJS framework**, as this is the most common.

---

### 🔓 What You Will Learn

- How to **craft exploits that escape from the AngularJS sandbox**
- How to potentially use AngularJS features to **bypass Content Security Policy (CSP)**