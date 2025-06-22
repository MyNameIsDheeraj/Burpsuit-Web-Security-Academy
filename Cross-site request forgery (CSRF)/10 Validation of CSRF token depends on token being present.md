# 10. Validation of CSRF token depends on token being present

### 🔍 Description

Some applications correctly validate the CSRF token **when it is present**, but **skip the validation entirely if the token is omitted**.

---

### ⚠️ Vulnerability Explanation

In this situation, an attacker can **remove the entire parameter** containing the CSRF token (not just its value) to **bypass validation** and successfully deliver a **CSRF attack**.

---

### 📥 Sample Malicious Request

```
POST /email/change HTTP/1.1
Host: vulnerable-website.com
Content-Type: application/x-www-form-urlencoded
Content-Length: 25
Cookie: session=2yQIDcpia41WrATfjPqvm9tOkDvkMvLm

email=pwned@evil-user.net
```

---

### 💡 Key Point

> ✅ No csrf parameter is included in the request.
> 
> 
> If the application does not enforce CSRF validation when the token is missing, the attacker can exploit this to perform unauthorized actions on behalf of the user.
>