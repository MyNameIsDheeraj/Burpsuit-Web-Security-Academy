# 01. Lab: Basic SSRF against the local server

### 🧪 Lab Summary

This lab has a **Stock Check** feature that fetches data from an internal system.

Your goal is to **perform an SSRF attack** to access the **admin interface** at `http://localhost/admin` and **delete the user `carlos`**.

---

### 🧩 Step-by-Step Solution

### 🔒 1. Attempt Direct Admin Access

- Go to `/admin` directly in the browser.
- ❌ Observe that **you can't access** the admin panel from the frontend.

---

### 📦 2. Intercept the Stock Check Request

- Visit **any product page**.
- Click **"Check stock"**.
- In **Burp Suite**, intercept the request.
- ➡️ **Send it to Repeater** for testing.

---

### 🌐 3. Deliver the SSRF Payload

- Modify the `stockApi` parameter to:
    
    ```
    http://localhost/admin
    ```
    
- 🔍 This should retrieve the **internal admin interface**.

---

### 🕸️ 4. Analyze the Admin Panel HTML

- Carefully read the HTML response.
- Locate the **delete user link**, which should look like:
    
    ```
    http://localhost/admin/delete?username=carlos
    ```
    

---

### 💥 5. Delete Carlos via SSRF

- Submit the above **delete URL** via the `stockApi` parameter:
    
    ```
    stockApi=http://localhost/admin/delete?username=carlos
    ```
    
- ✅ This will **trigger the SSRF**, resulting in the deletion of the target user.

---

### 🎉 Lab Solved!

You've successfully used a **Server-Side Request Forgery** vulnerability to:

- Bypass frontend restrictions
- Access a protected internal admin endpoint
- Trigger sensitive functionality (user deletion)

---

### 📽️ Community Walkthrough

🔗 [Watch Solution on YouTube](https://youtu.be/4oXH8qRqDPQ)