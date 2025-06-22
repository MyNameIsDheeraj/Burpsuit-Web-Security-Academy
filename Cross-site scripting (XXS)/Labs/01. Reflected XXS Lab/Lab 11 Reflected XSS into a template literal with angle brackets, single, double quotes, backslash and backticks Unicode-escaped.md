# Lab 11:Reflected XSS into a template literal with angle brackets, single, double quotes, backslash and backticks Unicode-escaped

This lab demonstrates a **reflected cross-site scripting (XSS) vulnerability** in the **search blog functionality**. The user input is reflected inside a **JavaScript template string** on the page.

---

## 🎯 Objective

Execute JavaScript code inside a template string to trigger:

```jsx
alert(1)
```

---

## 🔍 Background

The reflected data is processed inside a JavaScript template literal where:

- Angle brackets `<` and `>` are HTML-encoded.
- Single and double quotes `'` and `"` are HTML-encoded.
- Backticks ``` are escaped.

Despite this, JavaScript expressions inside `${...}` template placeholders can still be executed.

---

## 🛠️ Step-by-step Solution

1. **Send a test search query** — enter a random alphanumeric string in the search bar on the target site.
2. **Intercept and forward the request** — use Burp Suite’s Proxy tool to intercept and forward the request, then send it to Burp Repeater.
3. **Identify input reflection** — observe that your input is reflected inside a JavaScript template literal.
4. **Inject the payload** — replace the test string with this payload:
    
    ```jsx
    ${alert(1)}
    ```
    
5. **Verify the exploit** — right-click on the search results page, select **Copy URL**, and paste it into a new browser tab. Loading the page should trigger the `alert(1)` pop-up.

---

## ✅ Lab Solved

The execution of the `alert(1)` confirms the successful exploitation of reflected DOM XSS inside a JavaScript template string.

---

## 🎥 Community Video Solution

- [Watch here](https://youtu.be/y0onQRBnwMM)