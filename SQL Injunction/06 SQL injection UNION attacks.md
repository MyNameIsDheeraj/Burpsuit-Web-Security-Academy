# 06. SQL injection UNION attacks

### 🛠️ What is a UNION Attack?

When an application is vulnerable to **SQL injection** and query results are reflected in the application’s responses, attackers can use the `UNION` keyword to retrieve data from other tables in the database.

This technique is called a **SQL injection UNION attack**.

---

### How `UNION` Works

The `UNION` keyword lets you execute one or more additional `SELECT` queries and append their results to the original query’s results.

Example:

```sql
SELECT a, b FROM table1 UNION SELECT c, d FROM table2
```

- Returns a single result set with **two columns**.
- The result contains values from columns `a` and `b` in `table1` **and** columns `c` and `d` in `table2`.

---

### Key Requirements for a Successful `UNION` Query

1. 📊 **Same Number of Columns**
    
    Each individual `SELECT` query must return the **same number of columns**.
    
2. 🔄 **Compatible Data Types**
    
    The data types in corresponding columns must be **compatible** between queries.
    

---

### How to Carry Out a UNION Attack

To perform a successful SQL injection UNION attack, you must:

- 🔍 Discover how many columns the original query returns.
- 🧩 Identify which columns can hold data from the injected query based on compatible data types.

---

> ⚠️ Note:
> 
> 
> Ensuring these requirements are met is essential for your injected query to execute without errors and retrieve meaningful data.
>