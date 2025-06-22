# 17. Bypassing SameSite Lax restrictions using GET requests

### 🧠 **Concept Overview**

Even with **`SameSite=Lax`** restrictions in place, CSRF attacks can still be successful **under certain conditions** — especially when:

- The server accepts **GET** requests for actions that should be protected.
- The browser sends **cookies on top-level navigation GET requests** (which `Lax` allows).
- Or, the server is **not strict** about enforcing HTTP methods.

---

### 🎯 **Real-World Scenario**

Some web applications allow actions like payments or email changes via GET requests — often unintentionally. If the server uses cookies with `SameSite=Lax`, these cookies **will be sent** in:

- Top-level navigations (like a user clicking a link or being redirected)
- Requests using the **GET** method

### 🚨 **Simple GET-Based CSRF Attack**

If the endpoint performs a sensitive action using GET, you can exploit it like this:

```html
<script>
  document.location = 'https://vulnerable-website.com/account/transfer-payment?recipient=hacker&amount=1000000';
</script>
```

- The victim's browser navigates to the malicious URL.
- If `SameSite=Lax` is in effect, the **session cookie is sent**.
- If the server doesn't block GET-based state changes, the action is completed.

---

### 🧪 **Method Override Exploits**

Even if GET isn’t allowed directly, **some frameworks allow method overriding** via hidden form fields. This lets attackers **disguise a POST request as a GET**.

### 🧱 **Example: Symfony**

Symfony supports a special parameter: `_method`. If this is included in a form, the framework may **treat the request as if it's using the overridden method**.

```html
<form action="https://vulnerable-website.com/account/transfer-payment" method="POST">
  <input type="hidden" name="_method" value="GET">
  <input type="hidden" name="recipient" value="hacker">
  <input type="hidden" name="amount" value="1000000">
</form>
```

### 🧩 **Other Frameworks**

Other frameworks (like Laravel, Spring, or Express) also support **method override mechanisms**, commonly via:

- `_method=PUT` or `_method=DELETE`
- Custom headers like `X-HTTP-Method-Override`

---

### ✅ **Mitigation Tips for Developers**

- Never allow sensitive actions (like payments, password changes) via **GET**.
- Enforce **strict method validation** server-side.
- Use **SameSite=Strict** for session cookies where feasible.
- Implement **robust CSRF tokens**, not just SameSite.