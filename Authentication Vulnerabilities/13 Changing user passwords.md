# 13. Changing user passwords

# 🔐 **Changing User Passwords**

📝 **Typical process:**

Changing your password usually involves:

1️⃣ Entering your **current password**

2️⃣ Entering your **new password twice** to confirm ✅

These pages rely on the **same process** for checking that **usernames and current passwords** match — just like a normal login page does.

💡 **This means** they can be vulnerable to the **same attack techniques** as a login page.

---

## ⚠️ **Why it can be dangerous**

Password change functionality can be **particularly dangerous** if:

- It allows an attacker to access it **without being logged in** as the victim 🔓
- For example, if the **username** is stored in a **hidden field** in the request form, an attacker might:
    - ✏️ Edit this value to **target arbitrary users**
    - 🕵️ Enumerate valid usernames
    - 💥 Brute-force passwords

---

🔍 **Takeaway:**

Treat password change functionality with **the same security measures** as a login page plus **additional checks** to ensure only an authenticated user can perform the action.