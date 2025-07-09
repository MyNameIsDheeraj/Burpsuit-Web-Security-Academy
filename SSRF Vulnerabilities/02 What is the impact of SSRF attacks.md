# 02. What is the impact of SSRF attacks?

### 🚨 Unauthorized Access & Actions

A successful **Server-Side Request Forgery (SSRF)** attack can lead to:

- 🔐 **Unauthorized actions** or **access to sensitive data**
- 📦 Impact on both the **vulnerable application** *and* other **back-end systems** that the application can reach

---

### 🖥️ Remote Code Execution

In some advanced cases, an SSRF vulnerability may allow:

- 🧨 **Arbitrary command execution**
    
    🔓 Turning a simple request flaw into full system compromise
    

---

### 🌍 Third-Party Attack Relay

An SSRF exploit that **connects to external third-party systems** can:

- 🎯 Perform **malicious outward attacks**
- 🎭 Make attacks appear as if they **originate from the victim organization’s server**

> ⚠️ This can damage reputation, create legal risk, and undermine trust.
> 

---

🛡️ **Pro Tip:** Always treat SSRF seriously — it’s not just an internal recon tool, but a potential launchpad for full compromise.