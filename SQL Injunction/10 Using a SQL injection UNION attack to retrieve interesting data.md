# 10. Using a SQL injection UNION attack to retrieve interesting data

### 🔍 Prerequisites

Before retrieving data, ensure that:

- ✅ You have determined the **number of columns** returned by the original query.
- ✅ You have identified which columns can **hold string data**.

---

### 📌 Example Scenario

Suppose that:

- 📄 The original query returns **two columns**, both compatible with string data.
- 🔐 The injection point is a **quoted string** within the `WHERE` clause.
- 🧑‍💻 The database contains a table called `users` with columns `username` and `password`.

---

### 💥 Injection Payload

You can retrieve the contents of the `users` table by submitting the following input:

```sql
' UNION SELECT username, password FROM users--
```

---

### 🧠 Important Note

To perform this attack, you **must know**:

- The name of the **table** (`users`)
- The names of the **columns** (`username`, `password`)

---

### 🗺️ Exploring the Database Structure

Without prior knowledge of the schema, you would need to **guess** table and column names.

However, all modern databases offer ways to **explore their structure** and find out:

- 📋 What tables exist
- 📦 What columns those tables contain