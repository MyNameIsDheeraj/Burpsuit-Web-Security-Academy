# 03. SQL injection in different parts of the query

Most **SQL injection vulnerabilities** occur within the `WHERE` clause of a `SELECT` query. This type is the most familiar to experienced testers.

---

## 📌However, SQL injection can occur in many places within different query types, including:

- `UPDATE` statements
    
    Vulnerabilities may exist within the updated values or the `WHERE` clause.
    
- `INSERT` statements
    
    Vulnerabilities may appear within the inserted values.
    
- `SELECT` statements
    
    Vulnerabilities can occur within:
    
    - The table or column name
    - The `ORDER BY` clause