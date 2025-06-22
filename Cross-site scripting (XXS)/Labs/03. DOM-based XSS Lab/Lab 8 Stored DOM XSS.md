# Lab 8: Stored DOM XSS

This lab demonstrates a **stored DOM-based XSS vulnerability** in the **blog comment feature**. The vulnerability arises from JavaScript incorrectly sanitizing user input before injecting it into the DOM.

---

## 🎯 Objective

Exploit the vulnerability to execute the following:

```jsx
alert(1)
```

---

## 💥 Key Insight

The site attempts to prevent XSS using:

```jsx
input.replace("<", "&lt;").replace(">", "&gt;");
```

But this only replaces the **first instance** of `<` and `>` due to the use of string literals instead of global regular expressions.

---

## 🛠️ Solution Steps

### 1. ✍️ Submit the Payload

Post a comment using the following input:

```html
<><img src=1 onerror=alert(1)>
```

### 2. 📜 Why This Works

- The initial `<>` pair triggers the **`replace()` function**, consuming the **first `<` and `>`**.
- The **second set** (`<img ...>`) is **left untouched**, so it renders as raw HTML.
- The `onerror=alert(1)` triggers JavaScript execution when the image fails to load.

This bypasses the faulty sanitization and successfully leads to stored DOM-based XSS.

---

## ✅ Lab Solved

Once the comment is saved and viewed again, your payload executes and triggers `alert(1)`, completing the lab.

---

## 📽️ Community Reference

- 🎥 [Video Walkthrough](https://youtu.be/kjPwxAPt318)