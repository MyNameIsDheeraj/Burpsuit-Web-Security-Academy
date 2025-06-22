# Lab 6: DOM XSS in AngularJS expression with angle brackets and double quotes HTML-encoded

## 🔍 Understanding the Vulnerability

- The application uses AngularJS, which processes HTML elements with the `ng-app` attribute.
- AngularJS expressions inside double curly braces `{{ }}` are evaluated as JavaScript expressions.
- When user input is placed inside AngularJS expressions without proper sanitization, an attacker can inject malicious code.
- This bypasses typical HTML encoding since angle brackets `< >` are encoded but curly braces `{{ }}` are not.

---

## 🪜 Step-by-Step Solution

### 1️⃣ Initial Test

- Enter a random alphanumeric string into the search box.
- View the page source to confirm that your input is placed inside an AngularJS `ng-app` directive.

### 2️⃣ Inject Malicious AngularJS Expression

- Enter the following payload into the search box to execute JavaScript:

```
{{$on.constructor('alert(1)')()}}
```

- Click **Search**.

---

## ✅ Expected Result

- The injected AngularJS expression triggers the `alert(1)` function.
- This confirms the successful execution of JavaScript via AngularJS expression injection.

---

## 🎥 Community Solutions Video

- [Watch the Exploit Walkthrough](https://youtu.be/QpQp2JLn6JA)