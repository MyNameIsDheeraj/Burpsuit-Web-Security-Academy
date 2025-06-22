# 14. How to test for DOM-based cross-site scripting

## ⚙️ Automated Testing

Most DOM XSS vulnerabilities can be quickly and reliably detected using **Burp Suite’s web vulnerability scanner**.

---

## 🧑‍💻 Manual Testing Using Browser Developer Tools

To manually test for DOM XSS, use a browser with developer tools such as **Google Chrome**, and work through each available **source** individually.

---

### 🔍 Testing HTML Sinks

1. Place a random alphanumeric string into the source (e.g., `location.search`).
2. Open Developer Tools and inspect the **live HTML DOM** to locate where your string appears.
    
    > Note: The browser’s View Source option won’t work for DOM XSS testing because it shows the original HTML, not the DOM modified by JavaScript.
    > 
3. In Chrome Developer Tools, use `Ctrl+F` (or `Cmd+F` on Mac) to search for your string in the DOM.
4. For each occurrence, identify the **context** (e.g., inside a double-quoted attribute).
5. Refine your input to test how it is processed, for example:
    - If inside double quotes, try injecting double quotes to break out of the attribute.

---

**💡 Browser Behavior Notes:**

- Chrome, Firefox, and Safari URL-encode `location.search` and `location.hash`.
- IE11 and legacy Microsoft Edge do **not** URL-encode these sources.
- If data is URL-encoded before processing, an XSS attack is less likely to succeed.

---

### 🧩 Testing JavaScript Execution Sinks

Testing JavaScript execution sinks is more complex because your input might not appear directly in the DOM.

1. Use the **JavaScript debugger** to analyze how the source data flows in the page's scripts.
2. Search the page’s JavaScript code for references to the source variable (e.g., `location`).
    - In Chrome Developer Tools, use `Ctrl+Shift+F` (or `Cmd+Alt+F` on Mac) to search all loaded scripts.
3. Add breakpoints where the source is accessed to follow the flow of data.
4. Track variables that receive values from the source, searching for their usage and whether they are passed to sinks.
5. Inspect variable values by hovering over them during debugging to see if the payload reaches a sink.
6. Refine your input accordingly to attempt a successful XSS attack.

---

### ⚡ Testing for DOM XSS Using DOM Invader

Identifying and exploiting DOM XSS in real-world applications can be tedious, especially when dealing with complex or minified JavaScript.

If you use **Burp’s browser**, you can leverage its built-in **DOM Invader extension**, which automates much of this process and helps you identify potential DOM XSS vulnerabilities quickly.