# 01. API recon

### 🔍 Identifying API Endpoints

**API endpoints** are the specific locations where an API receives requests related to a certain resource on its server.

📘 **Example:**

```
GET /api/books HTTP/1.1
Host: example.com
```

➡️ **Endpoint:** `/api/books`

This request retrieves a list of books from the library.

Another example:

```
GET /api/books/mystery HTTP/1.1
```

➡️ **Endpoint:** `/api/books/mystery`

This retrieves a list of **mystery books**.

---

### 🛠️ Understanding How to Interact with Endpoints

Once endpoints are identified, the next step is to determine **how to construct valid HTTP requests** to interact with them properly.

Here's what you should explore:

---

### 📥 Input Data

- ✅ **Compulsory parameters**
- 🆗 **Optional parameters**

Understanding what data the API expects helps in crafting effective requests and identifying potential weaknesses.

---

### ⚙️ Supported HTTP Methods

- 🔄 `GET`, `POST`, `PUT`, `DELETE`, etc.
- 📦 Supported **media formats** (e.g., JSON, XML)

Knowing the supported methods allows you to test the full range of interactions with the API.

---

### 📉 Rate Limits & 🔐 Authentication

- ⏱️ **Rate limits:** How often can you make requests before being blocked?
- 🔑 **Authentication mechanisms:**
    - API keys
    - Bearer tokens
    - OAuth flows

Identifying these constraints is crucial for proper and ethical testing.

---

🧠 By following these steps, you can effectively understand and test any API's surface, preparing you to find potential vulnerabilities or inefficiencies.