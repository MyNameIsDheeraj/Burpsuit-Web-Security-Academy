# 02. API documentation

> APIs are usually documented so that developers know how to use and integrate with them.
> 

---

### 🧠 **Types of Documentation**

📄 **Human-Readable Documentation**

- Designed for developers to understand how to use the API.
- Includes:
    - 🧾 Detailed explanations
    - 💡 Examples
    - 🧪 Usage scenarios

🤖 **Machine-Readable Documentation**

- Designed for software to process and automate tasks like:
    - 🔄 API integration
    - ✅ Validation
- Typically written in structured formats like:
    - `JSON`
    - `XML`

---

### 🌐 **Public Availability**

- API documentation is often **publicly available** – especially if it's designed for external developers.
- ✅ **Always start your recon** by reviewing the documentation when it's accessible.

---

## 🔍 **Discovering API Documentation**

Even if documentation isn’t publicly exposed, you may still be able to **find it by exploring applications** that use the API.

### 🕵️‍♂️ **Tools to Use**

- 🧪 **Burp Scanner** – to crawl the API automatically.
- 🌐 **Burp Browser** – to manually browse and analyze endpoints.

---

### 🔎 **Look for These Endpoints**

Examples of endpoints that may refer to documentation:

```
/api
/swagger/index.html
/openapi.json
```

---

### 📂 **Investigating Resource Paths**

If you find a resource endpoint like:

```
/api/swagger/v1/users/123
```

Then be sure to also investigate:

```
/api/swagger/v1
/api/swagger
/api
```

---

### 🚀 **Pro Tip with Intruder**

Use a list of **common paths** to discover hidden documentation with **Burp Intruder**.

---

You can use a range of **automated tools** to analyze any **machine-readable API documentation** that you find. 🛠️

### 🧪 **Burp Suite Tools**

🛰️ **Burp Scanner**

- Crawl and audit **OpenAPI** documentation
- Supports **JSON** or **YAML** formats

🔍 **OpenAPI Parser BApp**

- Parse **OpenAPI documentation** directly
- Useful for exploring structured API specs

---

### 🔧 **Specialized API Testing Tools**

You may also be able to use a **specialized tool** to test the documented endpoints, such as:

📬 **Postman**

🧼 **SoapUI**

> These tools help you interactively test endpoints using the information provided in machine-readable API docs. 💡
>