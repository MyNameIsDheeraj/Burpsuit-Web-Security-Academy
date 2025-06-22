# 28. Constructing an advanced AngularJS sandbox escape

### 🚧 Handling Restrictions on Quotes

Sometimes, sites **restrict usage of single (`'`) or double (`"`) quotes**, making sandbox escapes more challenging.

In this case, you’ll need to:

- Use functions like `String.fromCharCode()` to generate characters dynamically.
- Bypass AngularJS restrictions on accessing the `String` constructor by using the **constructor property of a string**.
- Find a way to **create a string without using quotes** to start the process.

---

### ⚙️ Alternative Execution: Using the `orderBy` Filter

In a typical sandbox escape, you use `$eval()` to execute JavaScript payloads.

- But in the lab below, `$eval()` is **undefined**.
- Luckily, you can use AngularJS’s `orderBy` filter as an alternative.

---

### 🔎 How the `orderBy` Filter Works

The syntax:

```
[123] | orderBy:'Some string'
```

Explanation:

- The `|` operator in AngularJS indicates a **filter operation** (not bitwise OR).
- The array `[123]` is passed into the `orderBy` filter.
- The colon `:` specifies the filter’s argument, in this case a string.
- Though normally used for sorting, `orderBy` **accepts an expression**, allowing you to pass a payload.