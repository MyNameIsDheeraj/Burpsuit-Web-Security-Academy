# 13. What is DOM-based cross-site scripting?

# 🌐 DOM-Based Cross-Site Scripting (DOM XSS)

In this section, we'll describe **DOM-based cross-site scripting (DOM XSS)**, explain how to find DOM XSS vulnerabilities, and talk about how to exploit DOM XSS with different **sources** and **sinks**.

---

## ❓ What is DOM-Based XSS?

DOM-based XSS vulnerabilities usually arise when JavaScript takes data from an **attacker-controllable source**, such as the URL, and passes it to a **sink** that executes dynamic code, such as:

- `eval()`
- `innerHTML`
- `document.write()`

This allows attackers to inject and execute **malicious JavaScript**, which can lead to actions like:

- Stealing session tokens
- Defacing content
- Performing actions on behalf of users (e.g. CSRF-like effects)

---

## 🚀 How DOM-Based XSS Works

To exploit a DOM-based XSS vulnerability, an attacker must:

1. Inject data into a **source** (e.g. `location.search`)
2. Ensure the value is **used unsafely** by JavaScript
3. Trigger **execution** via a vulnerable **sink**

This happens **entirely on the client-side** — without any request reaching the server.

---

## 🌍 Common Sources

DOM XSS originates from **user-controllable sources** like:

| Source | Description |
| --- | --- |
| `window.location` | Full URL |
| `location.search` | Query string |
| `location.hash` | URL fragment (after `#`) |
| `document.referrer` | Referring page URL |
| `document.URL` | Entire URL |
| `window.name` | Name of the current browser window |
| `postMessage()` | Inter-window communication |

---

## ⚠️ Dangerous Sinks

These are the **execution points** where malicious input leads to XSS:

| Sink | Risk Type |
| --- | --- |
| `innerHTML` | Renders raw HTML |
| `outerHTML` | Replaces element + HTML parsing |
| `document.write()` | Inserts HTML into the document |
| `element.insertAdjacentHTML` | Inserts raw HTML |
| `eval()` / `setTimeout("...")` | Executes JS code |
| `location.href = "javascript:..."` | Executes JS if attacker controls it |

---

## 🛠️ Exploiting DOM XSS

To exploit a DOM-based XSS:

- Identify the **data flow** from **source → sink**
- Craft a payload like:
    
    ```
    https://example.com/page?input=<img src=1 onerror=alert(1)>
    
    ```
    
- If the page inserts `input` using `.innerHTML`, the payload will execute

---

## 🧪 Testing for DOM XSS

### 🔍 Manual Testing Steps

1. **Inject a unique string** into known sources (e.g., `?test=abc123`)
2. Use **browser DevTools** to inspect where that string appears in the DOM
3. Look for unsafe usage in sinks like `.innerHTML`
4. Refine your input to break out of the context and inject JavaScript

### 🧰 Tools

- **Chrome DevTools** (for breakpoints, DOM inspection)
- **Burp Suite + DOM Invader** (automates source/sink detection)
- **DOMPurify** (used for remediation)

---

## 🧬 Sources & Sinks in 3rd Party Libraries

### 🌀 jQuery Examples

```
$('#element').html(userInput);        // unsafe
$('#link').attr("href", userInput);  // can be unsafe with "javascript:"
$(window).on('hashchange', function() {
  var el = $(location.hash);         // vulnerable in older jQuery versions
});

```

### 🌀 AngularJS

AngularJS enables code execution inside:

```html
<div ng-app>
  {{constructor.constructor('alert(1)')()}}
</div>

```

- Any interpolation using `{{ }}` can become an **execution sink** if not properly sanitized.

---

## 📦 Stored vs Reflected DOM XSS

| Type | Description |
| --- | --- |
| **Reflected** | Server reflects attacker-controlled input into the response, and JS on the page processes it in a sink |
| **Stored** | Attacker input is stored server-side (e.g., in a comment), and reflected into a future page where JavaScript dangerously processes it |

---

## 🧱 Defense Strategies

✅ **Use Safe DOM APIs**:

- `textContent`, `setAttribute`, and `createElement` over `innerHTML`, `eval`, etc.

✅ **Sanitize input**:

- Use libraries like `DOMPurify`

✅ **Implement CSP**:

- Content Security Policy to block inline scripts and `eval()`

✅ **Avoid unsafe libraries** or keep them **patched** (e.g., jQuery, AngularJS)

---

## 📌 Summary

- DOM XSS happens when **client-side JavaScript** uses **untrusted input** in a **dangerous context**
- Unlike traditional XSS, DOM XSS does **not involve server response modification**
- Testing involves **tracking taint flow** from **source → sink**
- Tools like **Burp Suite's DOM Invader** can accelerate detection