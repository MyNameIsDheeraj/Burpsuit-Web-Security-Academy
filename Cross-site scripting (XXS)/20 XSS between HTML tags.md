# 20. XSS between HTML tags

### 🌐 Understanding the Context

When the **XSS context is text between HTML tags**, you need to introduce **new HTML tags** that are capable of triggering JavaScript execution.

---

### 🚀 Useful Payloads to Execute JavaScript

Here are some commonly used payloads:

```jsx
<script>alert(document.domain)</script>
<img src=1 onerror=alert(1)>
```

🧪 These examples inject executable code into otherwise safe text contexts by wrapping them in **scriptable HTML elements**.