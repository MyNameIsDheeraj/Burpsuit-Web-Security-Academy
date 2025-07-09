# 08. Testing for server-side parameter pollution in the query string

## 💉 **Server-Side Parameter Pollution (SSPP)**

> Server-side parameter pollution occurs when user input is embedded into server-side requests to internal APIs without proper encoding.
> 

This can allow attackers to:

- 🛠️ Override existing parameters
- 🔀 Modify application behavior
- 🔓 Access unauthorized data

---

## 🔍 **What to Test**

You can test **any user-controlled input** for parameter pollution, including:

- 🔹 Query parameters
- 🔹 Form fields
- 🔹 Headers
- 🔹 URL path parameters

---

## 📘 **Server-Side Parameter Pollution Example**

### 🧪 Request:

```
GET /userSearch?name=peter&back=/home

```

➡️ This results in an internal API call like:

```
GET /users/search?name=peter&publicProfile=true

```

---

## ✂️ **Truncating Query Strings**

You can use a **URL-encoded `#`** character (`%23`) to try and **truncate** the server-side query. Add a recognizable string after it for easier tracking.

🧪 Try:

```
GET /userSearch?name=peter%23foo&back=/home

```

➡️ Internal API becomes:

```
GET /users/search?name=peter#foo&publicProfile=true

```

> ⚠️ Note: Always URL-encode the #, otherwise the browser interprets it as a fragment and it won’t be sent to the server.
> 

📌 **Observe the response:**

- If **user `peter` is returned**, the query may have been truncated.
- If you get an **"Invalid name"** error, the server may be treating `foo` as part of the username → no truncation occurred.

✅ Successful truncation **may bypass requirements** like `publicProfile=true`, allowing access to **private profiles**.

---

## 💣 **Injecting Invalid Parameters**

Use a **URL-encoded `&`** (`%26`) to attempt **parameter injection**.

🧪 Try:

```
GET /userSearch?name=peter%26foo=xyz&back=/home

```

➡️ Internal API becomes:

```
GET /users/search?name=peter&foo=xyz&publicProfile=true

```

🔍 **Check the response**:

- If **unchanged**, the `foo=xyz` param may have been **accepted but ignored**
- You’ll need **further testing** to fully assess the behavior

---

## ✅ **Injecting Valid Parameters**

Once you know how to inject, try adding **valid parameters**.

📌 If you've discovered a hidden `email` parameter, try:

```
GET /userSearch?name=peter%26email=foo&back=/home

```

➡️ Internal API becomes:

```
GET /users/search?name=peter&email=foo&publicProfile=true

```

🔍 Review the response to determine how the **new parameter is parsed**.

---

## 🔁 **Overriding Existing Parameters**

To confirm SSPP, try **injecting a duplicate parameter** with the **same name**.

🧪 Try:

```
GET /userSearch?name=peter%26name=carlos&back=/home

```

➡️ Internal API becomes:

```
GET /users/search?name=peter&name=carlos&publicProfile=true

```

🧠 **Result depends on back-end tech:**

| Framework | Behavior |
| --- | --- |
| **PHP** | Uses **last param only** → returns **carlos** |
| **ASP.NET** | Combines → **peter,carlos** → error possible |
| **Node.js** | Uses **first param only** → still **peter** |

🎯 **If override works**, try:

```
name=administrator

```

→ This may let you **access admin accounts** or sensitive data!