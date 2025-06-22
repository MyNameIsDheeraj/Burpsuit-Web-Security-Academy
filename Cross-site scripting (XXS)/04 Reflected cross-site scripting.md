# 04. Reflected cross-site scripting

Reflected XSS is the simplest variety of cross-site scripting. It arises when an application receives data in an HTTP request and includes that data within the immediate response in an unsafe way.

---

### Example of a Reflected XSS Vulnerability

**Normal request:**

```
https://insecure-website.com/status?message=All+is+well.

```

**Response:**

```html
<p>Status: All is well.</p>

```

---

### Attacker’s Crafted Request

```
https://insecure-website.com/status?message=<script>/*+Bad+stuff+here...+*/</script>

```

**Resulting response:**

```html
<p>Status: <script>/* Bad stuff here... */</script></p>

```

---

### Impact

If a user visits the attacker-crafted URL, the attacker’s script runs in the user's browser under the user’s session context. This enables the attacker to perform any action or retrieve any data accessible to the user.