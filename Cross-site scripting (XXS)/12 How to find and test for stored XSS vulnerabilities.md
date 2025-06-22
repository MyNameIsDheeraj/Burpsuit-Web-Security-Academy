# 12. How to find and test for stored XSS vulnerabilities

Many stored XSS vulnerabilities can be found using **Burp Suite's web vulnerability scanner**.

---

### ⚠️ Manual Testing Challenges

Testing for stored XSS vulnerabilities **manually** can be challenging. You need to test all relevant:

- **Entry points** — ways attacker-controllable data can enter the application
- **Exit points** — places where that data might appear in application responses

---

### 🚪 Entry Points Into Application Processing

Entry points include:

- Parameters or other data within the **URL query string** and **message body**
- The **URL file path**
- **HTTP request headers** that might not be exploitable in reflected XSS
- Any **out-of-band routes** where an attacker can deliver data into the application

> The routes depend on the application functionality, for example:
> 
> - A webmail app processes emails
> - An app displaying Twitter feeds processes third-party tweets
> - A news aggregator includes data from other websites

---

### 🧾 Exit Points for Stored XSS

Exit points are all possible **HTTP responses** returned to any kind of application user in any situation.

---

### 🔗 Linking Entry Points to Exit Points

The first step is to **locate the links** where data submitted at an entry point is emitted from an exit point. Challenges include:

- Data submitted at any entry point could be emitted from **any exit point**
    
    (e.g., user display names might appear in obscure audit logs visible only to some users)
    
- Stored data may be **overwritten** by other application actions
    
    (e.g., recent searches replaced as users perform new searches)
    

---

### 🧩 Comprehensive Testing Strategy

Testing every permutation individually — submitting a value, navigating to the exit point, and checking if it appears — is usually impractical for apps with many pages.

---

### ✅ Practical Testing Approach

1. Work **systematically through entry points**, submitting specific values.
2. Monitor the application's responses to detect where the submitted value appears.
3. Pay special attention to relevant features like blog post comments.
4. Confirm whether the data is **stored across requests** or simply reflected immediately.

---

### 🧪 Final Verification

Once links between entry and exit points are identified:

- Specifically test each link for stored XSS vulnerabilities
- Determine the **context** where the stored data appears in the response
- Test appropriate candidate XSS payloads for that context

At this point, the testing approach resembles that for [reflected XSS vulnerabilities](https://portswigger.net/web-security/cross-site-scripting/reflected).