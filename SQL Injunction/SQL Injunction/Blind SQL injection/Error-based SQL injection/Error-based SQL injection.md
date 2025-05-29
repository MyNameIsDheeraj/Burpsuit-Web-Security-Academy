# Error-based SQL injection

**Error-based SQL injection** leverages error messages from the database to extract or infer sensitive data — even when direct query output is not shown (i.e., blind scenarios).

---

## 🔎 How It Works

Depending on how the application and database are configured, you can:

### ✅ Trigger Boolean-Based Errors

- Use SQL expressions that intentionally **cause an error** when a condition is met.
- Similar to **boolean-based blind SQL injection**, but the difference in behavior is due to the **presence or absence of an error** rather than a visible message like "Welcome back."

🧪 **Example:**

```sql
' AND 1=CASE WHEN (SELECT SUBSTRING(password,1,1) FROM users WHERE username='admin')='s' THEN 1/0 ELSE 1 END--
```

- If the first character is `'s'`, the query causes a **divide-by-zero error**.
- If not, the query runs fine.
- You can detect this via error messages or HTTP status codes.

➡️ See: **Exploiting blind SQL injection by triggering conditional errors**

---

### 🔍 Force Verbose Errors to Leak Data

- Some DBMSs return **detailed error messages** including the results of subqueries or functions.
- This can be abused to make a **normally-blind** vulnerability **output data directly**.

🧪 **Example in MySQL:**

```sql
' AND (SELECT 1 FROM (SELECT COUNT(*), CONCAT((SELECT version()),FLOOR(RAND()*2)) x FROM information_schema.tables GROUP BY x) y)--
```

- This causes a **duplicate entry error** in the `GROUP BY`, which **leaks the DB version** in the error message.

➡️ See: **Extracting sensitive data via verbose SQL error messages**

---

## 🧠 Notes

- These techniques **bypass blind limitations** by abusing how the server **handles and displays errors**.
- They often require **detailed understanding of the DBMS behavior** (MySQL, PostgreSQL, Oracle, etc.).
- Some web servers and WAFs **suppress error messages**, reducing effectiveness.