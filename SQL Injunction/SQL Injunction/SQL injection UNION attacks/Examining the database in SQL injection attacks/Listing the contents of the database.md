# Listing the contents of the database

## 🧠 Exploring the Database Structure via `information_schema`

Most database types (except Oracle) provide a special set of views called the **`information_schema`**, which reveals metadata about the database.

---

## 📋 Listing Tables in the Database

You can query the `information_schema.tables` view to list all tables:

```sql
SELECT * FROM information_schema.tables
```

### 📤 Sample Output:

```
TABLE_CATALOG  TABLE_SCHEMA  TABLE_NAME  TABLE_TYPE
=====================================================
MyDatabase     dbo           Products    BASE TABLE
MyDatabase     dbo           Users       BASE TABLE
MyDatabase     dbo           Feedback    BASE TABLE
```

🔍 **This tells us** the database contains three tables:

- `Products`
- `Users`
- `Feedback`

---

## 🧱 Listing Columns in a Specific Table

You can query `information_schema.columns` to list all columns of a specific table:

```sql
SELECT * FROM information_schema.columns WHERE table_name = 'Users'
```

### 📤 Sample Output:

```
TABLE_CATALOG  TABLE_SCHEMA  TABLE_NAME  COLUMN_NAME  DATA_TYPE
=================================================================
MyDatabase     dbo           Users       UserId       int
MyDatabase     dbo           Users       Username     varchar
MyDatabase     dbo           Users       Password     varchar
```

✅ This shows the columns inside the `Users` table along with their data types.