# 13. CSRF token is simply duplicated in a cookie

## 🔍 Vulnerability Description

In a further variation on the preceding vulnerability, some applications **do not maintain any server-side record of tokens** that have been issued. Instead, they **duplicate each token within a cookie and a request parameter**.

When the subsequent request is validated, the application **simply verifies that the token submitted in the request parameter matches the value submitted in the cookie**.

> This is sometimes called the "double submit" defense against CSRF and is advocated because it is simple to implement and avoids the need for any server-side state.
> 

---

## 📬 Example Request

```
POST /email/change HTTP/1.1
Host: vulnerable-website.com
Content-Type: application/x-www-form-urlencoded
Content-Length: 68
Cookie: session=1DQGdzYbOJQzLP7460tfyiv3do7MjyPw; csrf=R8ov2YBfTYmzFyjit8o2hKBuoIjXXVpa

csrf=R8ov2YBfTYmzFyjit8o2hKBuoIjXXVpa&email=wiener@normal-user.com
```

## ⚔️ Exploitation Technique

In this situation, the attacker can again perform a **CSRF attack** if the website contains **any cookie setting functionality**.

- The attacker **doesn't need to obtain a valid token of their own**.
- They simply **invent a token** (perhaps in the required format, if that is being checked).
- Then, they **leverage the cookie-setting behavior** to place their cookie into the **victim's browser**.
- Finally, they **feed their token to the victim** in their **CSRF attack**.