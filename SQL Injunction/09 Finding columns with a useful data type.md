# 09. Finding columns with a useful data type

### 🎯 Purpose

A **SQL injection UNION attack** enables you to retrieve the results from an injected query.

The **interesting data** you want to retrieve is usually in **string form**.

👉 This means you must identify **columns that can store string data** in the original query.

---

### 🔢 Step-by-Step: Finding Compatible Columns

Once you know the **number of columns** returned by the original query, you can test each column for string compatibility using this approach:

**Example (for a query returning 4 columns):**

```sql
' UNION SELECT 'a',NULL,NULL,NULL--
' UNION SELECT NULL,'a',NULL,NULL--
' UNION SELECT NULL,NULL,'a',NULL--
' UNION SELECT NULL,NULL,NULL,'a'--
```

---

### ⚠️ Error Behavior

If a column **cannot hold string data**, the query will throw an error like:

```
Conversion failed when converting the varchar value 'a' to data type int.
```

---

### ✅ Success Criteria

If no error occurs and the application’s response includes:

- The injected string (like `'a'`)
- Or shows additional content

👉 Then the tested column **can hold string data** and is suitable for **retrieving results** from your injected query.

---