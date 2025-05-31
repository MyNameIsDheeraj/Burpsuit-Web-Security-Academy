# 9. Validation of CSRF token depends on request method

🔍 Some applications correctly validate the CSRF token when the request uses the **POST method**, but **skip the validation** when the **GET method** is used.

🚨 In this situation, an attacker can **switch to the GET method** to bypass the validation and successfully deliver a **CSRF attack**.

### 💥 **Example Exploit Using GET Method**

```
GET /email/change?email=pwned@evil-user.net HTTP/1.1
Host: vulnerable-website.com
Cookie: session=2yQIDcpia41WrATfjPqvm9tOkDvkMvLm
```

🧨 The lack of CSRF validation on GET requests allows the attacker to make unauthorized changes using a simple URL.

## 🖥️ 9.1 Lab: CSRF where token validation depends on request method

### ▶️ [Click Here](https://github.com/MyNameIsDheeraj/Burpsuit-Web-Security-Academy/blob/main/Cross-site%20request%20forgery%20(CSRF)/0%20Labs/9%201%20Lab%20CSRF%20where%20token%20validation%20depends%20on%20request%20method.md)


This lab contains the main source code files and exercises.
