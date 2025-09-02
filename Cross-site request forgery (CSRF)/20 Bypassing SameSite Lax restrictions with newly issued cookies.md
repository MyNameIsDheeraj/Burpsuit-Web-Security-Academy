# 20. Bypassing SameSite Lax restrictions with newly issued cookies

## 🔎 Background

- If a website **doesn't include a SameSite attribute** when setting a cookie, Chrome **automatically applies Lax** restrictions by default.
- ⚠️ To avoid breaking **Single Sign-On (SSO)** mechanisms, Chrome **doesn't enforce these restrictions for the first 120 seconds** on top-level POST requests.
- ⏳ This means there is a **two-minute window** in which users may be susceptible to **cross-site attacks**.

> 📝 Note:
> 
> 
> This **two-minute window** does **NOT** apply to cookies that were explicitly set with `SameSite=Lax`.
> 

---

## ⚔️ Attack Strategy

It’s somewhat **impractical** to time the attack to fall **within this short window**.

👉 However, if you can find a **gadget** on the site that enables you to **force the victim to be issued a new session cookie**, you can **preemptively refresh their cookie** before launching the **main attack**.

🔑 **Example:**

Completing an **OAuth-based login flow** may result in a **new session each time** since the OAuth service doesn’t necessarily know whether the user is still logged in to the target site.

---

## 🎯 Practical Exploitation

To **trigger the cookie refresh** without requiring the victim to log in manually:

1. Use a **top-level navigation** → ensures cookies associated with the current **OAuth session** are included.
2. Redirect the victim **back to your site** so you can launch the **CSRF attack**.

⚡ Alternatively:

- Trigger the refresh from a **new tab** so the victim doesn’t leave the page.
- 🚫 Browsers block popups unless opened via **manual interaction**.

---

## 💻 Example Code

❌ Blocked by browser (popup will not open):

```jsx
window.open('https://vulnerable-website.com/login/sso');
```

✅ Allowed when wrapped in an **onclick event**:

```jsx
window.onclick = () => {
    window.open('https://vulnerable-website.com/login/sso');
}
```

---

## 🛡️ Key Takeaways

- 🔄 **SameSite=Lax cookies** have a **120s grace period** when newly issued.
- 🕵️‍♂️ Attackers can exploit this by **refreshing the victim’s session cookie** via OAuth or similar flows.
- 🎭 Popups for triggering flows must be **user-driven** (e.g., click events).