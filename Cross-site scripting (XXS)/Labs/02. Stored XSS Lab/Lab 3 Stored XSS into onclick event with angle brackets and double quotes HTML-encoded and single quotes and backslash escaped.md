# Lab 3: Stored XSS into onclick event with angle brackets and double quotes HTML-encoded and single quotes and backslash escaped

## 🎯 Lab Goal

Submit a comment where the **Website field** injects JavaScript into an `onclick` event handler so that clicking the **author’s name** triggers an `alert(1)` popup.

---

## 🛠️ Solution Steps

### 1️⃣ Submit a Test Comment

- In the comment form, input a **random alphanumeric string** (e.g., `testXSS`) into the **Website** field.
- Use **Burp Suite**:
    - Intercept the submission request
    - Send it to **Burp Repeater**

---

### 2️⃣ Observe Reflection in Response

- In your browser, visit the post page to see your comment
- Use Burp again to:
    - Intercept the GET request for the post
    - Send it to **Repeater**
- 🔍 **Note:** The random string is reflected inside an `onclick` attribute — indicating an injection vector.

---

### 3️⃣ Inject the XSS Payload

- Resubmit the comment with the following payload in the **Website** field:

```
http://foo?&apos;-alert(1)-&apos;

```

This cleverly injects the `alert(1)` code within the `onclick` handler context.

---

### 4️⃣ Trigger the Payload

- Right-click on the **name above your comment**
- Select **"Copy Link Address"** or **"Copy URL"**
- Paste the URL into your browser's address bar and press **Enter**
- ✅ **Result:** Clicking the name triggers the `alert(1)` popup — confirming successful XSS.

---

## 🎥 Community Walkthrough

📺 [Watch solution on YouTube](https://youtu.be/-4ia_L-uLGY)