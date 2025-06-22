# 17. DOM XSS combined with reflected and stored data

DOM-based cross-site scripting (XSS) vulnerabilities occur entirely on the **client side**, typically involving JavaScript that reads attacker-controlled input and processes it through an insecure sink.

---

## 🧼 1. Pure DOM-Based XSS

A **pure DOM XSS vulnerability** is *fully self-contained* within a single client-side page:

- No interaction with the server is needed.
- A script reads input from a browser-exposed source (like `window.location`) and passes it to a sink.

### 🔁 Example

```jsx
const userInput = new URLSearchParams(window.location.search).get('name');
document.write('<div>' + userInput + '</div>');

```

📌 If a user visits:

```
https://vulnerable.site/page?name=<script>alert(1)</script>

```

…the script writes unescaped HTML to the DOM.

---

## 🔁 2. Reflected DOM-Based XSS

In a **reflected DOM XSS**, the vulnerability is still client-side, but part of the exploit chain **involves the server**:

- The server reflects user-supplied data into the HTML.
- JavaScript on the client side later **reads** that reflected data and **writes it to a dangerous sink**.

### 🧪 Example

Server-side:

```html
<script>
  let user = "{{username}}";
  eval('var data = "' + user + '"');
</script>
```

If the server reflects unvalidated user input into `{{username}}`, and the attacker supplies:

```
" ; alert(document.domain); //
```

…it becomes:

```jsx
eval('var data = "' + '"; alert(document.domain); //' + '"');
```

This executes the payload inside `eval()`—a dangerous sink.

---

## 💾 3. Stored DOM-Based XSS

In **stored DOM XSS**, data is:

1. Submitted to the server by an attacker.
2. Stored on the backend (e.g., database, user profile).
3. Later included in a page where a **client-side script** sends it to a dangerous sink.

This is **client-side processing of server-stored data**.

### 📝 Example

Server stores a comment like:

```json
{
  "author": "<img src=1 onerror=alert(document.cookie)>"
}
```

Later page includes:

```jsx
element.innerHTML = comment.author;
```

Result: the stored payload is inserted unsafely into the DOM and the malicious code executes.

---

## 📌 Summary of DOM XSS Types

| Type | Server Involvement | Data Lifecycle | Example Sink |
| --- | --- | --- | --- |
| **Pure DOM XSS** | ❌ None | Read from browser source | `innerHTML`, `eval()` |
| **Reflected DOM XSS** | ✅ Partial | Reflected from server → JS → sink | `eval('...')` |
| **Stored DOM XSS** | ✅ Yes | Stored on server → later used by JS | `element.innerHTML` |