# 23. How to prevent SQL injection

## 🛡️ Preventing SQL Injection with Parameterized Queries

You can prevent most instances of SQL injection by using **parameterized queries** instead of **string concatenation** within the query. These parameterized queries are also known as **"prepared statements"**.

---

### ❌ Vulnerable Code (Prone to SQL Injection)

The following code is **vulnerable** because the user input is **concatenated directly** into the query:

```java
String query = "SELECT * FROM products WHERE category = '"+ input + "'";
Statement statement = connection.createStatement();
ResultSet resultSet = statement.executeQuery(query);
```

---

### ✅ Secure Code (Using Prepared Statement

You can rewrite the code to **prevent user input** from interfering with the query structure:

```java
PreparedStatement statement = connection.prepareStatement("SELECT * FROM products WHERE category = ?");
statement.setString(1, input);
ResultSet resultSet = statement.executeQuery();
```

> 💡 Using prepared statements ensures that user input is treated strictly as data, not executable code.
> 

You can use **parameterized queries** for any situation where **untrusted input appears as data** within the query — including:

- The `WHERE` clause
- Values in an `INSERT` or `UPDATE` statement

However, **parameterized queries cannot** be used to handle untrusted input in other parts of the query, such as:

- **Table or column names**
- The **`ORDER BY`** clause

---

### ⚙️ Alternative Approaches for Non-Data Parts of Queries

For situations where untrusted data must appear in unsupported parts of a query, use these approaches instead:

- ✅ **Whitelisting** permitted input values
- ✅ Using **different logic** to deliver the required behaviour

---

### 🚫 Avoid This Common Pitfall

For a parameterized query to be effective in preventing SQL injection:

- The **SQL string must always be a hard-coded constant**.
- It must **never** contain **any variable data from any origin**.

> ⚠️ Do not decide case-by-case whether data is trusted and revert to string concatenation for seemingly safe cases.
> 

It's easy to **make mistakes** about the origin of data — or for **other code changes** to inadvertently **taint trusted data**.