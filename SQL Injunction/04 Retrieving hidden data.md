# 04. Retrieving hidden data

### 🛒Scenario

Imagine a shopping application that displays products in different categories. When the user clicks on the **Gifts** category, their browser requests the URL:

```
https://insecure-website.com/products?category=Gifts
```

This causes the application to make the following SQL query to retrieve relevant product details:

```sql
SELECT * FROM products WHERE category = 'Gifts' AND released = 1
```

---

### What this query does:

- 🔍 Retrieves **all details** ()
- 📦 From the `products` table
- 🏷️ Where the `category` is `'Gifts'`
- ✔️ And `released = 1` (only released products)

> The restriction released = 1 hides unreleased products, assumed to have released = 0.
> 

---

### Vulnerability: No SQL Injection Defense

The application **does not defend** against SQL injection attacks. This allows an attacker to modify the query by injecting malicious input.

---

### Example Attack 1: Commenting Out Part of the Query

Attacker crafts this URL:

```sql
https://insecure-website.com/products?category=Gifts'--
```

This produces the SQL query:

```sql
SELECT * FROM products WHERE category = 'Gifts'--' AND released = 1
```

---

### Explanation:

- `-` is an SQL comment indicator.
- Everything after `-` is ignored by the database.
- The condition `AND released = 1` is **removed** by commenting.
- Result: **All products are displayed**, including unreleased ones.

---

### Example Attack 2: Using OR Condition to Return All Products

Attacker uses this URL:

```
https://insecure-website.com/products?category=Gifts'+OR+1=1--
```

Resulting SQL query:

```sql
SELECT * FROM products WHERE category = 'Gifts' OR 1=1--' AND released = 1
```

---

### Explanation:

- The query returns all products where:
    - The `category` is `'Gifts'`, **or**
    - `1=1` (which is **always true**)
- So, the query returns **all products**, regardless of category or release status.

---

> ⚠️ Warning:
> 
> 
> Be careful when injecting conditions like `OR 1=1`. Applications often reuse request data in multiple queries. If your injected condition affects an `UPDATE` or `DELETE` query, it could lead to unintended data loss.
>