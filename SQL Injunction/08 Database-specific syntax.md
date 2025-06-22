# 08. Database-specific syntax

### 🛠️ Requirement on Oracle:

- Every `SELECT` query **must** use the `FROM` keyword and specify a valid table.
- Oracle provides a built-in table called `dual` for this purpose.

**Example of an injected query on Oracle:**

```sql
' UNION SELECT NULL FROM DUAL--
```

---

### 📝 About Comment Syntax:

- The payloads described use the **double-dash (`-`)** comment sequence to comment out the rest of the original query after the injection point.
- On **MySQL**, the double-dash **must be followed by a space** to work correctly.
- Alternatively, the **hash character (`#`)** can be used as a comment marker.

---

### 🔗 For More Details:

Check out the comprehensive [SQL injection cheat sheet](https://portswigger.net/web-security/sql-injection/cheat-sheet) for database-specific syntax and advanced techniques.