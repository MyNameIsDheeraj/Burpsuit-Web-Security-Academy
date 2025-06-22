# 19. Cross-site scripting contexts

## 🔍 Identifying the XSS Context

### 🧪 When Testing for [Reflected](https://portswigger.net/web-security/cross-site-scripting/reflected) and [Stored](https://portswigger.net/web-security/cross-site-scripting/stored) XSS

A key task is to **identify the XSS context**, which includes:

- 📍 **The location within the response** where attacker-controllable data appears.
- 🛠️ **Any input validation or other processing** that is being performed on that data by the application.

---

### 🎯 What’s Next?

Based on these details, you can then:

- Select one or more **candidate XSS payloads**
- 🧪 **Test** whether they are effective in triggering XSS behavior

---

> 📝 Note
> 
> 
> We have built a comprehensive [XSS cheat sheet](https://portswigger.net/web-security/cross-site-scripting/cheat-sheet) to help with testing web applications and filters.
> 
> ✅ You can **filter by events and tags**
> 
> ✅ See which vectors require **user interaction**
> 
> ✅ Explore **AngularJS sandbox escapes** and many more sections to support **XSS research**
>