# 4. How to construct a CSRF attack

### 🧱 **Why use a generator?**

Manually creating the HTML needed for a CSRF exploit can be **cumbersome**, especially when:

- The request has **many parameters**
- There are **quirks** in the request formatting

---

### 🚀 **Use the CSRF PoC Generator in Burp Suite Pro**

Burp Suite Professional makes this easy with a built-in tool:

---

### 📋 **Steps to Generate a CSRF Proof of Concept (PoC):**

1. **Select the request**
    
    Locate the request anywhere in **Burp Suite Professional** that you want to test or exploit.
    
2. **Right-click the request**
    
    Choose:
    
    `Engagement tools` → `Generate CSRF PoC`
    
3. **Burp generates the exploit HTML**
    
    This HTML will trigger the **selected request**, except:
    
    - **Cookies are omitted** in the HTML (but they’ll be **added automatically** by the victim's browser)
4. **Customize the PoC**
    
    You can **tweak options** in the CSRF PoC generator to:
    
    - Fine-tune the request
    - Handle unusual or quirky behaviors in the HTTP request
5. **Deploy and test**
    - Copy the generated HTML into a **web page**
    - Open it in a **browser where the user is logged in** to the target site
    - **Test** if the intended request is made and the desired action is completed




## 🖥️ [4.1 Lab: CSRF vulnerability with no defenses](https://github.com/MyNameIsDheeraj/Burpsuit-Web-Security-Academy/blob/main/Cross-site%20request%20forgery%20(CSRF)/0%20Labs/4%201%20Lab%20CSRF%20vulnerability%20with%20no%20defenses.md)


This lab contains the main source code files and exercises.

