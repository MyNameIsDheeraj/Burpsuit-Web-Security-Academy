# 02. How does XSS work?

### 🛠️ Mechanism of Attack

**Cross-site scripting works by manipulating a vulnerable website so that it returns malicious JavaScript to users.**

When the malicious code executes inside a victim's browser, the attacker can **fully compromise their interaction** with the application.

---

### ⚙️ Step-by-Step Breakdown

1. 🎯 **Target Identification**
    
    A web application with an input/output handling flaw is identified.
    
2. ✍️ **Injection**
    
    The attacker inserts **malicious JavaScript** (e.g., through a form, URL, or comment field).
    
3. 🔁 **Execution**
    
    The vulnerable site **reflects or stores** the malicious script and sends it to users' browsers.
    
4. 💥 **Impact**
    
    Once executed in the browser, the attacker can:
    
    - Hijack sessions
    - Deface the interface
    - Steal sensitive data

---

### 🔒 Reminder

Mitigation requires **proper input validation**, **output encoding**, and the use of **Content Security Policy (CSP)**.

![cross-site-scripting.svg](Img/cross-site-scripting.svg)