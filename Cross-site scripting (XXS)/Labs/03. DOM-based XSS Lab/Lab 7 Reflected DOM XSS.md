# Lab 7: Reflected DOM XSS

## 🎯 Objective

This lab demonstrates a **reflected DOM-based XSS vulnerability**. In this type of attack, the **server reflects input** from the request back into the response, and **client-side JavaScript** later uses it **unsafely**, eventually writing it into a **dangerous sink** like `eval()`.

Exploit the DOM XSS vulnerability to trigger the `alert()` function.

---

## 🛠️ Step-by-Step Solution

### 1. 🔎 Trigger a Request with a Test String

- In the target lab website, use the **search bar** to enter a test string like:
    
    ```
    XSS
    ```
    

### 2. 📡 Intercept the Request in Burp Suite

- Open **Burp Suite** → **Proxy** tab → Ensure **Intercept is ON**.
- Forward the request after interception.
- Observe the **JSON response** containing the test string.

### 3. 🧬 Analyze JavaScript Usage

- In the **Site Map**, locate and inspect the file:
    
    ```
    searchResults.js
    ```
    
- You'll see the JSON is **parsed using `eval()`**, which is **inherently unsafe**.

### 4. 🧪 Identify Injection Weakness

- Test different payloads in the search bar to see how characters are escaped.
- You’ll find:
    - **Double quotes** (`"`) are escaped
    - But **backslashes** (`\`) are **not**

---

## 💣 Exploit Payload

Enter the following string into the **search bar**:

```
\"-alert(1)}//
```

### 💡 How It Works

The input breaks out of the string context and injects raw JavaScript:

```
{"searchTerm":"\\"-alert(1)}//", "results":[]}
```

- `\\"` → Escaped backslash becomes literal `\`
- `\"` → Breaks out of the string
- `alert(1)` → Executes JavaScript
- `}//` → Closes object early and comments out the rest

This results in **`alert(1)` being executed**.

---

## ✅ Lab Solved

After submitting the payload and seeing the alert pop up, the lab marks as **solved**.

---

## 📽️ Community Reference

- 🎥 [Video Solution on YouTube](https://youtu.be/bg_xH4Dp-6E)