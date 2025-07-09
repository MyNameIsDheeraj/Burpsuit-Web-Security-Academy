# 09. Testing for server-side parameter pollution in REST paths

## 🧪 Testing for Server-Side Parameter Pollution in REST Paths

---

### 📌 REST Path Example

In a RESTful API, parameter **names and values** may appear in the **URL path** rather than the query string.

### Example:

```
/api/users/123

```

🔍 This path breaks down into:

- `/api` → **Root API endpoint**
- `/users` → **Resource** (e.g., users)
- `/123` → **Parameter** (e.g., user ID)

---

## 🎯 Real-World Example

An application allows profile editing using:

```
GET /edit_profile.php?name=peter

```

This results in a **server-side request** to:

```
GET /api/private/users/peter

```

---

## 🛡️ Attack Vector: REST Path Manipulation

An attacker may try to **manipulate server-side URL path parameters** to exploit internal APIs.

🧪 Test this using **path traversal sequences** like:

```
GET /edit_profile.php?name=peter%2f..%2fadmin

```

➡️ This might generate a server-side request like:

```
GET /api/private/users/peter/../admin

```

---

## 🔄 Server Behavior

If the server-side client or backend API performs **path normalization**, this may resolve to:

```
/api/private/users/admin

```

✅ This could **bypass access controls** and allow access to another user’s data (like an admin account).

---

### ⚠️ Reminder:

Always **URL-encode special characters** like `/` (`%2f`) and `..` to ensure the request is properly handled by the application during testing.

---

Let me know if you'd like this content exported to **Markdown**, **HTML**, or integrated into tools like **Docsify**, **MkDocs**, or **Notion**!