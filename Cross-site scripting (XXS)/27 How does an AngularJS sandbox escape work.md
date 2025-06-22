# 27. How does an AngularJS sandbox escape work?

### 🔍 What Is a Sandbox Escape?

A sandbox escape tricks the sandbox into **treating a malicious expression as benign**.

---

### 🚨 The Well-Known `charAt()` Escape

This escape uses a **modified `charAt()` function** globally within an expression:

```jsx
'a'.constructor.prototype.charAt=[].join
```

- Initially, AngularJS did **not prevent this modification**.
- The attack overwrites `charAt()` with the `[].join` method, causing `charAt()` to return **all characters** sent to it, rather than just one.

---

### 🧩 How the Bypass Works

Due to AngularJS’s `isIdent()` function logic, which compares what it expects to be a single character against multiple characters, the function **always returns `true`**, because:

- Single characters are always less than multiple characters in comparison.

Example:

```jsx
isIdent = function(ch) {
    return ('a' <= ch && ch <= 'z' || 'A' <= ch && ch <= 'Z' || '_' === ch || ch === '$');
}
isIdent('x9=9a9l9e9r9t9(919)')
```

### 💥 Consequence: Arbitrary Code Injection

Once `isIdent()` is fooled:

- You can inject malicious JavaScript
- Example payload: `$eval('x=alert(1)')`
- AngularJS treats every character as an identifier, allowing arbitrary JS execution

> ⚠️ Note: $eval() is required here because the modified charAt() affects code only at execution time.
> 

---

### 📖 Further Reading

PortSwigger Research has [broken the AngularJS sandbox comprehensively, multiple times](https://portswigger.net/research/xss-without-html-client-side-template-injection-with-angularjs).