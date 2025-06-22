# 10. Impact of stored XSS attacks

If an attacker can control a script that is executed in the victim's browser, then they can typically **fully compromise** that user. The attacker can carry out any of the actions that are applicable to the impact of [reflected XSS vulnerabilities](https://portswigger.net/web-security/cross-site-scripting/reflected).

---

### 🔑 Key Difference Between Reflected and Stored XSS

In terms of exploitability, the key difference between **reflected** and **stored** XSS is:

- A **stored XSS** vulnerability enables attacks that are **self-contained within the application itself**.
    
    The attacker does **not** need to find an external way of inducing other users to make a particular request containing their exploit. Rather, the attacker places their exploit into the application and simply waits for users to encounter it.
    

---

### ⏳ Timing and User State

The self-contained nature of stored cross-site scripting exploits is especially important when an XSS vulnerability affects **only logged-in users**.

- If the XSS is **reflected**, the attack must be **fortuitously timed**: a user must make the attacker’s crafted request **while logged in** to be compromised.
- If the XSS is **stored**, the user is **guaranteed** to be logged in when they encounter the exploit, as the malicious payload is embedded within the application itself.

---

### 📖 Further Reading

> Read more:
> 
> 
> [Exploiting cross-site scripting vulnerabilities](https://portswigger.net/web-security/cross-site-scripting/exploiting)
>