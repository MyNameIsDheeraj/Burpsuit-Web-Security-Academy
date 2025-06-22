# 31. How to prevent client-side template injection vulnerabilities

### 🚫 Best Practices

- **Avoid using untrusted user input** to generate templates or expressions whenever possible.
- If unavoidable, **filter out template expression syntax** from user input *before* embedding it within client-side templates.

---

### ⚠️ Important Note on HTML Encoding

- **HTML-encoding alone is insufficient** to prevent client-side template injection attacks.
- This is because frameworks typically **HTML-decode relevant content first**, before locating and executing template expressions.