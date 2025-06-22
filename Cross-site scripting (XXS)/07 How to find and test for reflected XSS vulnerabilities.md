# 07. How to find and test for reflected XSS vulnerabilities

## 🔍 Detecting Reflected Cross-site Scripting (XSS) Vulnerabilities

The vast majority of **reflected cross-site scripting (XSS)** vulnerabilities can be found **quickly and reliably** using **Burp Suite's web vulnerability scanner**.

### 🛠️ Manual Testing Workflow

Testing for reflected XSS vulnerabilities manually involves the following structured steps:

---

### 1. ✅ **Test every entry point**

Test separately **every entry point** for data within the application's HTTP requests. This includes:

- Parameters or other data in the **URL query string**
- **Message body** content
- The **URL file path**
- Relevant **HTTP headers**

> 🔒 Note: XSS-like behavior that only triggers via certain HTTP headers may not be exploitable in practice.
> 

---

### 2. 🔡 **Submit random alphanumeric values**

- Use **unique random values** for each entry point.
- These values should:
    - Be **short**, alphanumeric
    - Be **long enough** (≈8 characters) to prevent accidental matches
- Tools:
    - Use [**Burp Intruder’s number payloads**](https://portswigger.net/burp/documentation/desktop/tools/intruder/payloads/types#numbers) for random hex values
    - Use [**grep payload settings**](https://portswigger.net/burp/documentation/desktop/tools/intruder/configure-attack/settings#grep-payloads) to auto-flag responses that reflect your value

---

### 3. 📄 **Determine the reflection context**

Once the value is reflected in the response, identify **where and how** it is reflected:

- Inside text between **HTML tags**
- Inside a **tag attribute** (quoted or unquoted)
- Inside **JavaScript strings**
- Anywhere else in the page’s structure

---

### 4. ⚡ **Test a candidate payload**

- Based on the context, insert a **test XSS payload**.
- Use [**Burp Repeater**](https://portswigger.net/burp/documentation/desktop/tools/repeater) to modify and replay requests.
- Best practice:
    - Leave the original random value
    - Add the payload **before or after** the value
    - Set the random value as **search term** to quickly find its location in the response

---

### 5. 🔁 **Test alternative payloads**

If your candidate payload is **blocked or modified**, try:

- Encoding tricks
- Payload restructuring
- Context-specific techniques

📚 For more techniques, see: [XSS contexts guide](https://portswigger.net/web-security/cross-site-scripting/contexts)

---

### 6. 🌐 **Test the attack in a browser**

- Transfer the payload to a **real browser**:
    - Paste the URL in the address bar
    - Modify the request in [**Burp Proxy’s intercept view**](https://portswigger.net/burp/documentation/desktop/tools/proxy/intercept-messages)
- Use simple code like:
    
    ```
    alert(document.domain)
    
    ```
    
    to visibly confirm execution (a popup should appear if successful).