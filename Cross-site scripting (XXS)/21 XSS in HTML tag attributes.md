# 21. XSS in HTML tag attributes

### 🧪 Attribute-Based Injection Techniques

When the **XSS context is inside an HTML tag's attribute value**, there are a few ways to exploit it.

---

### 🔓 Terminate the Attribute and Inject a Script Tag

In some cases, you can **terminate the attribute**, **close the tag**, and **introduce a new script tag**:

```jsx
"><script>alert(document.domain)</script>
```

### 🧱 Bypassing Angle Bracket Restrictions with Event Handlers

Often, **angle brackets (`< >`) are blocked or encoded**, so you **can’t break out of the tag**. But if you can terminate the attribute value, you can inject a **new attribute** that creates a scriptable context:

```jsx
" autofocus onfocus=alert(document.domain) x="
```

This payload does the following:

- ✅ Creates an `onfocus` event to execute JavaScript when the element receives focus
- ✅ Adds the `autofocus` attribute to **automatically trigger `onfocus`**
- ✅ Appends `x="` to **gracefully repair** any following markup

---

### 🚀 Script Execution via Scriptable Attributes

Sometimes, the context is inside an attribute that **already supports script execution**, like the `href` attribute of an anchor tag.

In this case, you **don’t need to close the attribute**, just use a **scriptable protocol**:

```jsx
<a href="javascript:alert(document.domain)">
```

### 🎮 Exploiting Attributes in Non-Scriptable Tags Using Access Keys

You may encounter sites that **encode angle brackets but still allow attribute injection** — even in tags that **don’t typically fire events**, like:

```jsx
<link rel="canonical" href="..." accesskey="x" onfocus=...>
```

✅ **Access keys** allow you to bind elements to keyboard shortcuts

✅ Combined with **`onfocus`**, this can lead to XSS — **even in hidden or passive tags**

> 🧪 In the next lab, you’ll experiment with accesskey usage and exploit a canonical tag.
> 
> 
> 💡 [You can exploit XSS in hidden input fields using a technique invented by PortSwigger Research](https://portswigger.net/research/xss-in-hidden-input-fields)
>