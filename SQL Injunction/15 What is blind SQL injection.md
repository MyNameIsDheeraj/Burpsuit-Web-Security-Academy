# 15. What is blind SQL injection?

**Blind SQL Injection** occurs when an application is vulnerable to SQL injection, **but**:

- ❌ The HTTP responses **do not reveal** the results of the SQL query.
- ❌ No **database error details** are shown in the response.

---

## ❌ Why Common Techniques Fail

Techniques like:

- `UNION SELECT` attacks
- `ORDER BY` column counting
- Direct error-based injection

…**rely on visible responses**, such as query results or error messages in the browser.

Since blind SQL injection hides these outputs, those techniques **won’t work.**

---

## ✅ But It’s Still Exploitable

Even without visible clues, you **can still exploit** blind SQL injection:

- 🔁 **Boolean-based attacks** (true/false conditions)
- ⏱️ **Time-based attacks** (like `SLEEP` or `WAITFOR DELAY`)
- 🔤 **Out-of-band attacks** (e.g., DNS or HTTP exfiltration)

These alternative methods allow attackers to **infer** data, even if it isn’t directly returned.