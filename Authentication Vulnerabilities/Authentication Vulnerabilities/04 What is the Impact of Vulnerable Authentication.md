# 04. What is the Impact of Vulnerable Authentication?

Authentication vulnerabilities can be one of the **most critical issues** in web security.

---

### 🛡️ Unauthorized Account Access

> The impact of authentication vulnerabilities can be severe.
> 
- If an attacker **bypasses authentication** or **brute-forces** their way into another user's account,
    
    🔓 **they gain access to all data and functionality** that the compromised account has.
    

---

### 👑 High-Privilege Account Takeover

- If they are able to compromise a **high-privileged account**, such as a **system administrator**:
    
    ⚠️ **They could take full control over the entire application**
    
    🏗️ And potentially **gain access to internal infrastructure**.
    

---

### 📁 Even Low-Privileged Accounts Matter

> Even compromising a low-privileged account might still grant an attacker access to data they shouldn’t have.
> 
- 📊 For example, **commercially sensitive business information**
- 🧭 It might also allow access to **additional internal pages**, which could increase the **attack surface**

---

### 🧨 Internal Pages = Hidden Dangers

- 🔒 **High-severity attacks** are often **not possible** from **publicly accessible pages**
- 🧬 But they **may be possible** from **internal pages**, even with low privileges

---

🔐 **Always assume that any authentication bypass — even for the lowest-level user — is a gateway to deeper compromise.**