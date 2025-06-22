# 30. Bypassing a CSP with an AngularJS sandbox escape

### 🛠️ Problem

- The **previous CSP bypass vector won’t work** due to a **length restriction** in this lab.
- You need to find creative ways to **hide the `window` object** from AngularJS’s sandbox.

---

### 💡 Technique: Using `array.map()`

One effective technique is to use the `map()` function:

```jsx
[1].map(alert)
```

- `map()` accepts a function as an argument and calls it for every element in the array.
- This **bypasses the sandbox** because the `alert()` function is referenced **without explicitly referencing `window`**.

---

### 🎯 Goal

Try various ways of executing `alert()` **without triggering AngularJS’s `window` detection** to solve the lab.

---