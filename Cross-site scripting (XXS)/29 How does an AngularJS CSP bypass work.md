# 29. How does an AngularJS CSP bypass work?

### 🔄 How CSP Bypass Works

- CSP bypasses work similarly to **standard sandbox escapes**, but usually involve some **HTML injection**.
- When **CSP mode is active in AngularJS**, it:
    - Parses template expressions differently
    - Avoids using the `Function` constructor
- This means the **standard sandbox escape no longer works** in CSP mode.

---

### 🚫 CSP Restrictions and AngularJS Events

- CSP blocks **JavaScript events** depending on the policy.
- AngularJS defines its own **special events**, which can be used instead.

---

### 🔑 Using the Special `$event` Object

- Inside an AngularJS event, the special `$event` object references the **browser event object**.
- On Chrome, `$event.path` is a property containing an **array of objects** related to the event’s propagation path.
- The **last element is always the `window` object**, which can be leveraged for a sandbox escape.

---

### 🛠️ Exploit via `orderBy` Filter and `from()` Function

By passing the `$event.path` array to the `orderBy` filter, you can:

- Enumerate the array
- Access the last element (`window`)
- Execute global functions like `alert()`

Example:

```jsx
<input autofocus ng-focus="$event.path|orderBy:'[].constructor.from([1],alert)'">
```

- The `from()` function converts an object to an array and calls a function (here, `alert()`) on each element.
- This hides direct access to `window` from AngularJS’s sandbox parser, enabling malicious code injection.

---

### 📖 Further Reading

PortSwigger Research demonstrated a CSP bypass using AngularJS in just 56 characters:

👉 [AngularJS CSP Bypass in 56 Characters](https://portswigger.net/research/angularjs-csp-bypass-in-56-characters)