# 22. Validation of Referer depends on header being present

Some applications ✅ validate the **Referer header** only when it is **present** in requests,

but ❌ skip the validation if the header is **omitted**.

---

## 🎯 Exploitation Scenario

👉 In this case, an attacker can **craft a CSRF exploit** in such a way that the victim’s browser **drops the Referer header** in the request.

---

## 🛠️ How Attackers Achieve This

There are multiple ways to **strip or drop the Referer header**, but the easiest is by using a **META tag** inside the malicious HTML page hosting the CSRF attack:

```html
<meta name="referrer" content="never">

```

---

## ⚡ Impact

- The browser **omits the Referer header** 🚫
- The application **skips validation** 🛑
- The attacker’s CSRF attack **successfully bypasses Referer-based defenses** 🎯

---

## 🔐 Key Takeaway

📌 Relying on the **Referer header** for CSRF protection is **weak and unsafe**.

Better alternatives:

- ✅ Implement **CSRF tokens**
- ✅ Use **SameSite cookies**