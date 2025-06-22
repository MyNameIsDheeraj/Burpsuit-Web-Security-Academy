# 18. Which sinks can lead to DOM-XSS vulnerabilities?

# 🧪 DOM XSS Sinks

DOM-based XSS vulnerabilities occur when **attacker-controlled input** reaches a **sink** that interprets or executes that input insecurely.

---

## 📜 Native JavaScript Sinks

These are built-in DOM APIs commonly exploited in DOM XSS:

| Sink | Description |
| --- | --- |
| `document.write()` | Writes HTML directly into the page; can execute scripts. |
| `document.writeln()` | Same as `document.write()`, but adds a newline. |
| `element.innerHTML` | Injects raw HTML into an element (scripts generally ignored, but `onerror`/`onload` handlers fire). |
| `element.outerHTML` | Replaces the element and its contents—can run HTML with event handlers. |
| `element.insertAdjacentHTML()` | Inserts HTML at a position relative to the element. |
| `element.onevent` | Setting event handler attributes (`element.onclick = '...'`) can cause JS execution. |
| `document.domain` | Rarely a sink by itself, but mishandling can enable attacks in sandboxed frames. |

---

## 💻 JavaScript Execution Sinks (High-Risk)

These are especially dangerous because they **evaluate JavaScript directly**:

| Sink | Description |
| --- | --- |
| `eval()` | Executes arbitrary JavaScript—extremely dangerous. |
| `new Function()` | Similar to `eval`, compiles and runs JavaScript from a string. |
| `setTimeout()` | If the first argument is a string, it is evaluated as code. |
| `setInterval()` | Same as `setTimeout()` regarding strings. |
| `location.href` or `location.assign()` | May execute a `javascript:` URL if passed directly. |

---

## 🧩 jQuery Sinks

When user-controlled input reaches these **jQuery functions**, it can modify the DOM and potentially introduce XSS:

| jQuery Function | Risk Description |
| --- | --- |
| `.html()` | Injects raw HTML into an element. |
| `.append()` / `.prepend()` | Inserts content at the end or beginning of an element. |
| `.before()` / `.after()` | Inserts HTML before/after the element. |
| `.wrap()`, `.wrapAll()`, `.wrapInner()` | Wraps content in HTML—can be dangerous if input is HTML. |
| `.replaceWith()` / `.replaceAll()` | Replaces DOM content with new HTML. |
| `.add()` | Can add elements to a jQuery object—watch for user input. |
| `.animate()` | Can potentially be abused if animation properties are improperly parsed (rare, edge case). |
| `$.parseHTML()` / `jQuery.parseHTML()` | Parses a string into DOM elements—can result in XSS if user input is used. |

---

## ⚠️ Lesser-Known jQuery Internals (Rarely Abused)

These aren't common targets, but have had historical issues when misused:

Internal / Meta Functions

---

```
.init()
```

---

```
.constructor()
```

---

```
.has()
```

---

```
.index()
```

---

These are less likely to directly cause XSS, but could be abused in very specific or insecure custom wrappers.

---

## 🛡️ Tips for Securing DOM Sinks

- **Never** assign user-controlled data directly to dangerous sinks.
- Use `textContent` or `.innerText` instead of `.innerHTML` when inserting user data.
- Sanitize user input with a trusted HTML sanitizer (e.g., DOMPurify).
- Avoid using `eval()` or `setTimeout()` with string arguments.