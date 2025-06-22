# 25. What is the AngularJS sandbox?

### 🔐 Purpose

The AngularJS sandbox is a mechanism designed to **prevent access to potentially dangerous objects**, such as:

- `window`
- `document`

It also blocks access to risky properties, including:

- `__proto__`

---

### ⚠️ Security Perspective

- Although the **AngularJS team does not consider the sandbox a security boundary**,
- The **wider developer community generally disagrees**.

---

### 🔍 Bypassing the Sandbox

- Initially, bypassing the sandbox was challenging.
- However, **security researchers have discovered numerous bypass techniques** over time.

---

### 🕰️ Legacy Impact

- The sandbox was **removed in AngularJS version 1.6**.
- Many **legacy applications still use older AngularJS versions**, which **may remain vulnerable**.