# Lab: SQL injection attack, querying the database type and version on MySQL and Microsoft

This lab contains a SQL injection vulnerability in the product category filter. You can use a UNION attack to retrieve the results from an injected query.

To solve the lab, display the database version string.

### **Solution**

1. Use Burp Suite to intercept and modify the request that sets the product category filter.  
2. Determine the number of columns that are being returned by the query and which columns contain text data. Verify that the query is returning two columns, both of which contain text, 
using a payload like the following in the `category` parameter:

```sql
'+UNION+SELECT+'abc','def'#
```

![Screenshot from 2025-05-20 20-43-50.png](Lab%20SQL%20injection%20attack,%20querying%20the%20database%20ty%201efc172892ad805f8afde23649b2ea25/Screenshot_from_2025-05-20_20-43-50.png)

![Screenshot from 2025-05-20 20-44-07.png](Lab%20SQL%20injection%20attack,%20querying%20the%20database%20ty%201efc172892ad805f8afde23649b2ea25/Screenshot_from_2025-05-20_20-44-07.png)

3. Use the following payload to display the database version:

```sql
'+UNION+SELECT+@@version,+NULL#
```

![Screenshot from 2025-05-20 20-56-03.png](Lab%20SQL%20injection%20attack,%20querying%20the%20database%20ty%201efc172892ad805f8afde23649b2ea25/Screenshot_from_2025-05-20_20-56-03.png)

![Screenshot from 2025-05-20 20-56-34.png](Lab%20SQL%20injection%20attack,%20querying%20the%20database%20ty%201efc172892ad805f8afde23649b2ea25/Screenshot_from_2025-05-20_20-56-34.png)

![Screenshot from 2025-05-20 20-55-37.png](Lab%20SQL%20injection%20attack,%20querying%20the%20database%20ty%201efc172892ad805f8afde23649b2ea25/Screenshot_from_2025-05-20_20-55-37.png)

### **Community solutions**

> [https://youtu.be/4UxUpsCZQfI](https://youtu.be/4UxUpsCZQfI)
>