# 07. Determining the number of columns required

## 🔍 How to Determine the Number of Columns in a SQL Injection UNION Attack

When performing a **SQL injection UNION attack**, two effective methods help you discover how many columns the original query returns.

---

## Method 1: Using `ORDER BY` Clauses

You inject a series of `ORDER BY` clauses, incrementing the column index until an error occurs.

Example payloads (assuming the injection point is a quoted string in the `WHERE` clause):

```sql
' ORDER BY 1--
' ORDER BY 2--
' ORDER BY 3--
etc.
```

- This modifies the original query to order results by different columns.
- The column can be specified by its **index**, so you don’t need to know column names.
- When the index exceeds the actual number of columns, the database returns an error like:
    
    ```
    The ORDER BY position number 3 is out of range of the number of items in the select list.
    ```
    

### What happens on the application side?

- The app **might show the database error** in the HTTP response.
- It might issue a **generic error** or simply return **no results**.
- Any detectable change in response helps infer the **number of columns** returned.

---

## Method 2: Using `UNION SELECT` with NULL Values

You submit a series of `UNION SELECT` payloads with an increasing number of `NULL` values:

```sql
' UNION SELECT NULL--
' UNION SELECT NULL,NULL--
' UNION SELECT NULL,NULL,NULL--
etc.
```

- If the number of `NULL`s **does not match** the number of columns, you get an error like:
    
    ```
    All queries combined using a UNION, INTERSECT or EXCEPT operator must have an equal number of expressions in their target lists.
    ```
    
- `NULL` is used because it is **compatible with all common data types**, increasing the chance the payload will succeed when the column count is correct.

### What happens on the application side?

- The app might **show the database error**, a **generic error**, or **no results**.
- When the number of `NULL`s matches the columns, the database returns **an additional row** with all `NULL` values.
- Depending on the app’s behavior, you might see:
    - An **extra row in an HTML table** or extra content in the response.
    - A **NullPointerException** or other error triggered by null values.
    - Or no visible difference, making this method ineffective in some cases.

---

> 💡 Tip:
> 
> 
> Both methods rely on observing differences in the HTTP response. Even subtle changes can indicate how many columns are returned.
>