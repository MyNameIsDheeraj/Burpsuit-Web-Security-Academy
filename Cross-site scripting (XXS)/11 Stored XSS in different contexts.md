# 11. Stored XSS in different contexts

There are many different varieties of **stored cross-site scripting**. The location of the stored data within the application's response determines:

- What type of payload is required to exploit it
- How the impact of the vulnerability might vary

---

### 🔍 Influence of Validation and Processing

Additionally, if the application performs any **validation** or other **processing** on the data:

- **Before it is stored**, or
- **When the stored data is incorporated into responses**

this generally affects what kind of XSS payload is needed.

---

### 📖 Further Reading

> Read more:
> 
> 
> [Cross-site scripting contexts](https://portswigger.net/web-security/cross-site-scripting/contexts)
>