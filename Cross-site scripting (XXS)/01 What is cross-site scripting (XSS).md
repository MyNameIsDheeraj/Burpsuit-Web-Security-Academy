# 01. What is cross-site scripting (XSS)?

> Category: Web Security Vulnerability
> 
> 
> **Impact:** Session Hijacking, Data Theft, Full Application Compromise
> 
> **Risk Level:** 🔴 High
> 

---

### 🔍 What is Cross-Site Scripting?

**Cross-Site Scripting (XSS)** is a **web security vulnerability** that allows an attacker to compromise the interactions that users have with a vulnerable application.

---

### 🚧 Why is it Dangerous?

XSS enables an attacker to **circumvent the Same-Origin Policy** — a browser mechanism that segregates content from different websites — effectively breaking down a fundamental layer of web security.

---

### 🎭 What Can an Attacker Do?

- **Masquerade as the victim user**
- **Perform any actions** the user is permitted to do
- **Access user data** visible to the victim
- **Steal session tokens**, login credentials, or personal information

> ⚠️ If the victim has privileged access (like an admin or moderator), the attacker may gain full control over the application and its data.
> 

---

### 🧠 Key Takeaway

Cross-Site Scripting is one of the most critical vulnerabilities in web applications. It affects **user trust**, **application integrity**, and can lead to **severe data breaches** if not properly mitigated.