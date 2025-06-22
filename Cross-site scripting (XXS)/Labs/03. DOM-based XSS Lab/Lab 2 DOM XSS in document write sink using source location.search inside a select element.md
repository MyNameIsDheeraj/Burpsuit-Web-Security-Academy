# Lab 2: DOM XSS in document.write sink using source location.search inside a select element

## 🔍 Understanding the Vulnerability

- The page extracts the `storeId` parameter from the URL query string (`location.search`).
- This value is dynamically written into the page via `document.write()`.
- The output is inserted **inside a `<select>` element** as an `<option>`.
- Because the input is not properly sanitized or escaped, it's possible to break out of the `<select>` and inject arbitrary HTML/JS.

---

## 🪜 Steps to Exploit

### 1️⃣ Test Injection Point

- Navigate to a product page, e.g.:
    
    ```
    https://YOUR-LAB-ID.web-security-academy.net/product?productId=1&storeId=random123
    
    ```
    
- Observe that the value `random123` appears as an option in the stock checker dropdown.
- Use browser dev tools to **inspect the dropdown options** and confirm the injection point inside the `<select>` element.

### 2️⃣ Craft Your XSS Payload

Inject a payload that closes the `<select>` element and adds an image tag with an error handler:

```
"></select><img src=1 onerror=alert(1)>

```

### 3️⃣ Final Exploit URL

Visit the URL with the crafted payload as `storeId`:

```
https://YOUR-LAB-ID.web-security-academy.net/product?productId=1&storeId="></select><img src=1 onerror=alert(1)>

```

---

## ✅ Expected Behavior

- The injected `</select>` closes the dropdown prematurely.
- The `<img>` tag triggers an `onerror` event.
- An alert box with the number `1` pops up, confirming successful XSS.

---

## 🎥 Community Resources

> [YouTube Walkthrough 1](https://youtu.be/ojiOCfg-FXU)
[YouTube Walkthrough 2](https://youtu.be/UPvX_h3h_SI)
>