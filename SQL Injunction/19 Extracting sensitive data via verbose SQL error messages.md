# 19. Extracting sensitive data via verbose SQL error messages

Exactly! Verbose SQL error messages can be a goldmine for attackers because they often reveal:

- The **structure of the query** (e.g., how user input is embedded),
- The **database engine’s error details**,
- Sometimes even the **data itself**, when the error message contains content from the query results.

---

### Why Verbose Errors Help SQL Injection

Consider your example:

```sql
Unterminated string literal started at position 52 in SQL SELECT * FROM tracking WHERE id = '''. Expected char
```

- This error reveals you’re injecting inside a **single-quoted string** in a `WHERE` clause.
- You now know to properly **escape or close** quotes and **comment out** the rest of the query (`-` or `/* ... */`) to craft valid injection payloads.

---

### Using CAST() to Extract Data via Errors

By forcing type conversion errors, you can extract data from the database inside the error message itself.

Example injection:

```sql
CAST((SELECT example_column FROM example_table) AS int)
```

- If `example_column` contains a string like `"Example data"`, attempting to cast it to `int` causes an error like:

```
ERROR: invalid input syntax for type integer: "Example data"
```

- The error leaks the **content of `example_column`** directly.
- This works especially well in **blind SQL injection** cases where results are not normally displayed.

---

### Why This Matters

- **Bypassing output filtering**: Even if the app hides query results, error messages might show the data.
- **Circumventing length limits**: If the app limits response size or input length, error messages can still reveal data.
- **Discovering query context**: Helps in fine-tuning payloads by revealing how user input is embedded.

---

### Practical Tips

- Try injecting a type-casting payload (`CAST()`, `CONVERT()`, `TO_NUMBER()`, etc.) with subqueries selecting data.
- Trigger an incompatible cast to force the database to output the string data inside the error.
- Adjust based on database:
    - **PostgreSQL**: `CAST(... AS int)`
    - **MySQL**: Use `CAST(... AS SIGNED)`
    - **Oracle**: Use `TO_NUMBER(...)` or `TO_DATE(...)`