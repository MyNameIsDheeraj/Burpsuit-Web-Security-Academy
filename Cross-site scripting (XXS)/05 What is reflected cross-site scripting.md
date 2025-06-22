# 05. What is reflected cross-site scripting?

## 🧪 Reflected Cross-Site Scripting (XSS)

Reflected cross-site scripting (or XSS) arises when an application receives data in an HTTP request and includes that data within the immediate response in an unsafe way.

---

### 🔎 Scenario: Vulnerable Search Function

Suppose a website has a search function which receives the user-supplied search term in a URL parameter:

```
https://insecure-website.com/search?term=gift

```

The application echoes the supplied search term in the response to this URL:

```html
<p>You searched for: gift</p>

```

---

### ⚠️ Malicious Injection by an Attacker

Assuming the application doesn't perform any other processing of the data, an attacker can construct an attack like this:

```
https://insecure-website.com/search?term=<script>/*+Bad+stuff+here...+*/</script>

```

This URL results in the following response:

```html
<p>You searched for: <script>/* Bad stuff here... */</script></p>

```

---

### 🚨 Consequence

If another user of the application requests the attacker's URL, then the script supplied by the attacker will execute in the victim user's browser, in the context of their session with the application.