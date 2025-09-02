# 21. Bypassing Referer-based CSRF defenses

Some applications rely on the **HTTP Referer header** to defend against CSRF attacks.

They usually do this by checking that the request originated from the application's own domain.

⚠️ However, this approach is **less effective** and is often subject to bypasses.

---

## 📌 Referer Header

- The **HTTP Referer header** (misspelled in the HTTP spec 📜) is an **optional request header**.
- It contains the **URL of the web page** that linked to the requested resource.
- Browsers automatically add this header when:
    - A user clicks a **link** 🔗
    - A user submits a **form** 📝

---

## 🔒 Privacy & Manipulation

🔧 Various methods exist that allow the **linking page** to:

- Withhold the **Referer header** ❌
- Modify the **Referer header** ✏️

💡 This is often done intentionally for **privacy reasons** (to avoid leaking referrer URLs).

---

## 🚩 Why It’s Weak as a Defense

- Since the **Referer header** can be **controlled, stripped, or modified** by the client/browser,
- Attackers can often **bypass this defense** with relative ease.
- ✅ Safer defenses: **CSRF tokens** combined with **SameSite cookies**.