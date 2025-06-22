# 16. How does SameSite work?

### 📖 Background

Before the introduction of the **SameSite** mechanism, browsers would send cookies with **every request** to the domain that issued them — even if the request was initiated by a **third-party website**.

This behavior enabled attacks like **Cross-Site Request Forgery (CSRF)**, where malicious websites trick a victim's browser into making authenticated requests on another site.

---

## 🛡️ **What SameSite Does**

The `SameSite` attribute gives browsers and developers control over whether cookies are included in **cross-site requests**, helping protect against:

- CSRF
- Cross-site leaks
- Some CORS vulnerabilities

---

### ⚙️ How to Set SameSite

To configure this behavior, developers add the `SameSite` attribute in the `Set-Cookie` response header:

```
Set-Cookie: session=0F8tgdOhi9ynR1M9wa3ODa; SameSite=Strict
```

## 🌐 **Browser Support and Defaults**

All major browsers support these three SameSite levels:

- `Strict`
- `Lax`
- `None`

> 🔸 Since 2021, Chrome automatically applies SameSite=Lax to cookies that don’t explicitly set a restriction. Other browsers are expected to follow this proposed standard.
> 

---

## 📊 **SameSite Restriction Levels**

### 🔒 `SameSite=Strict`

- **Most secure** option.
- Cookie is **never** sent in cross-site requests.
- Sent **only** if the request originates from the **same site** currently shown in the address bar.

**Recommended for:**

- Session cookies
- Sensitive actions like authentication, user settings, etc.

**Drawback:**

- Can break legitimate cross-site functionality like login redirects or third-party integrations.

---

### ⚖️ `SameSite=Lax`

- Cookie is sent **only** if:
    - The request is a **top-level navigation** (e.g., user clicks a link), **and**
    - The request uses the **GET** method

**Not sent** for:

- POST requests
- Background requests (AJAX, iframes, image loads)

**Default in Chrome** if `SameSite` is not specified.

---

### 🌍 `SameSite=None`

- Cookie is sent **in all requests**, even those triggered by **third-party websites**.
- Completely disables SameSite restrictions.

**Use cases:**

- Cookies used in **third-party contexts** (e.g., analytics, social media widgets, CDN resources).

> ⚠️ Security requirement: Cookies with SameSite=None must also include Secure, or they will be rejected by modern browsers.
> 

```html
Set-Cookie: trackingId=abc123; SameSite=None; Secure
```

## 🔎 **Things to Watch For**

- Cookies set with `SameSite=None` or **no attribute at all** are worth investigating.
- Some developers **disable SameSite globally** to avoid broken functionality, even for sensitive cookies — a major security risk.
- The `Lax-by-default` model has **reduced CSRF exposure**, but **not eliminated** it.

---

## 📌 Summary

| Attribute | Sent on Cross-Site GET? | Sent on Cross-Site POST? | Best For |
| --- | --- | --- | --- |
| `Strict` | ❌ No | ❌ No | Secure sessions, sensitive user actions |
| `Lax` | ✅ Yes (GET + navigation) | ❌ No | Default behavior, minimal disruption |
| `None` + `Secure` | ✅ Yes | ✅ Yes | Third-party APIs, widgets, non-sensitive data |