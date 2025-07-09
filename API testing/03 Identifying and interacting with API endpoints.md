# 03. Identifying and interacting with API endpoints

You can also gather a lot of information by **browsing applications** that use the API.

> 💡 This is often worth doing even if you have access to the API documentation, as it may be inaccurate or out of date.
> 

---

### 🧭 **Tools for Exploration**

🛰️ **Burp Scanner**

- Crawl the application to identify endpoints.

🧑‍💻 **Burp's Browser**

- Manually investigate interesting parts of the attack surface.

---

### 🧠 **What to Look For**

- 🔗 **URL patterns** like `/api/`
- 📄 **JavaScript files** that reference hidden API endpoints
    - Burp Scanner extracts some automatically
    - 🧰 For deeper inspection, use the **JS Link Finder BApp**
    - 📝 You can also **manually review** JavaScript files in Burp

---

## 🔁 **Interacting with API Endpoints**

Once you've identified API endpoints:

🧪 Use **Burp Repeater** and **Burp Intruder**

➤ Observe API behavior

➤ Discover additional attack surface

🔍 Investigate how the API responds to:

- Changing the **HTTP method**
- Modifying the **media type**

🧾 **Pay close attention** to error messages and responses — they often reveal clues to help construct valid HTTP requests.

---

## 📬 **Identifying Supported HTTP Methods**

HTTP methods define the action to perform on a resource:

- `GET` – Retrieves data from a resource
- `PATCH` – Applies partial changes to a resource
- `OPTIONS` – Lists supported methods for a resource

> 🎯 An API endpoint may support multiple HTTP methods, so test all possible methods to reveal hidden functionality.
> 

---

### 🧪 **Example:**

For the endpoint:

```
/api/tasks
```

It may support:

```
GET /api/tasks       - Retrieves a list of tasks
POST /api/tasks      - Creates a new task
DELETE /api/tasks/1  - Deletes a task
```

✅ Use Burp Intruder's built-in **HTTP verbs list** to cycle through methods automatically.

> ⚠️ Note: When testing, target low-priority objects to avoid unintended consequences like deleting important data.
> 

---

## 🧾 **Identifying Supported Content Types**

API endpoints may behave differently depending on the **Content-Type** of the request:

🎯 Modifying the content type can help:

- 🔍 Trigger errors that reveal useful details
- 🛡️ Bypass flawed defenses
- ⚔️ Exploit processing inconsistencies (e.g., JSON vs XML)

🔧 To test this:

- Modify the `Content-Type` header
- Reformat the request body accordingly

🧰 Use the **Content Type Converter BApp** to automatically convert between `XML` and `JSON`.

---

## 🕵️ **Using Intruder to Find Hidden Endpoints**

Once you've found some initial endpoints:

🧨 Use **Burp Intruder** to uncover hidden ones.

### 🧪 Example:

If you've found:

```
PUT /api/user/update
```

You can try payloads like:

```
/api/user/delete
/api/user/add
```

➤ Add a payload to the `/update` portion with common function names.

---

### 🗂️ **Pro Tips**

- Use **wordlists** based on:
    - 📚 Common API naming conventions
    - 🏭 Industry-specific terms
    - 🔍 Clues from your **initial reconnaissance**