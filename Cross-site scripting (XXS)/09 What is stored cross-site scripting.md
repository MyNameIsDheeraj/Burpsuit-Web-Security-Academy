# 09. What is stored cross-site scripting?

# 📌 Stored Cross-Site Scripting (Persistent XSS)

Stored cross-site scripting (also known as second-order or persistent XSS) arises when an application receives data from an untrusted source and includes that data within its later HTTP responses in an unsafe way.

---

### 💬 Example: User Comments on a Blog Post

Suppose a website allows users to submit comments on blog posts, which are displayed to other users. Users submit comments using an HTTP request like the following:

```jsx
POST /post/comment HTTP/1.1
Host: vulnerable-website.com
Content-Length: 100

postId=3&comment=This+post+was+extremely+helpful.&name=Carlos+Montoya&email=carlos%40normal-user.net
```

---

### 📄 Application Response

After this comment has been submitted, any user who visits the blog post will receive the following within the application's response:

```jsx
<p>This post was extremely helpful.</p>
```

---

### ⚠️ Attack Scenario

Assuming the application doesn't perform any other processing of the data, an attacker can submit a malicious comment like this:

```jsx
<script>/* Bad stuff here... */</script>
```

Within the attacker's request, this comment would be URL-encoded as:

```jsx
comment=%3Cscript%3E%2F*%2BBad%2Bstuff%2Bhere...%2B*%2F%3C%2Fscript%3E
```

---

### 🖥️ Effect on Victim Users

Any user who visits the blog post will now receive the following within the application's response:

```jsx
<p><script>/* Bad stuff here... */</script></p>
```

The script supplied by the attacker will then execute in the victim user's browser, in the context of their session with the application.