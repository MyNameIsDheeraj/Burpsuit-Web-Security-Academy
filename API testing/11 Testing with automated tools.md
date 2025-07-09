# 11. Testing with automated tools

### 🛠️ Built-In Tools in Burp

Burp includes **automated tools** to help identify **Server-Side Parameter Pollution (SSPP)** vulnerabilities.

---

### 🔍 **Burp Scanner**

- ✅ **Automatically detects** suspicious **input transformations** during an audit.
- 🧪 These occur when:
    - The application **receives user input**
    - Then **transforms** it
    - Then performs **further processing**

> ⚠️ This behavior doesn't always mean a vulnerability — you'll need to manually test further.
> 

📖 **More Info:**

🔗 See the *Suspicious input transformation* issue definition *(insert actual link if used in a knowledge base)*

---

### 🧪 **Backslash Powered Scanner BApp**

💡 This Burp extension helps uncover **server-side injection vulnerabilities** by analyzing how the server reacts to special characters.

- 🧬 Inputs are classified into:
    - **Boring** 🟤 – likely safe
    - **Interesting** 🟡 – may need manual investigation
    - **Vulnerable** 🔴 – likely exploitable

> 🔍 You'll need to manually investigate interesting inputs using previously discussed techniques.
> 

📖 **More Info:**

📘 Backslash Powered Scanning: Hunting Unknown Vulnerability Classes – Whitepaper