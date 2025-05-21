# Lab: SQL injection UNION attack, retrieving multiple values in a single column

This lab contains a SQL injection vulnerability in the product category filter. The results from the query are returned in the application's response so you can use a UNION attack to retrieve data 
from other tables.The database contains a different table called `users`, with columns called `username` and `password`.

To solve the lab, perform a SQL injection UNION attack that retrieves all usernames and passwords, and use the information to log in as the `administrator` user.

### **Solution**

1. Use Burp Suite to intercept and modify the request that sets the product category filter. 

![2025-05-21_04-35.png](Lab%20SQL%20injection%20UNION%20attack,%20retrieving%20multipl%201efc172892ad80b68981e3c238b720d8/2025-05-21_04-35.png)

![2025-05-21_04-35_1.png](Lab%20SQL%20injection%20UNION%20attack,%20retrieving%20multipl%201efc172892ad80b68981e3c238b720d8/2025-05-21_04-35_1.png)

2. Determine the number of columns that are being returned by the query and which columns contain text data. Verify that the query is returning two columns, only one of which contain text,
 using a payload like the following in the `category` parameter:

```sql
'+UNION+SELECT+NULL,'abc'--
```

![2025-05-21_04-37.png](Lab%20SQL%20injection%20UNION%20attack,%20retrieving%20multipl%201efc172892ad80b68981e3c238b720d8/2025-05-21_04-37.png)

3. Use the following payload to retrieve the contents of the `users` table:

```sql
'+UNION+SELECT+NULL,username||'~'||password+FROM+users--
```

![2025-05-21_04-39.png](Lab%20SQL%20injection%20UNION%20attack,%20retrieving%20multipl%201efc172892ad80b68981e3c238b720d8/2025-05-21_04-39.png)

4. Verify that the application's response contains usernames and passwords.

![2025-05-21_04-40.png](Lab%20SQL%20injection%20UNION%20attack,%20retrieving%20multipl%201efc172892ad80b68981e3c238b720d8/2025-05-21_04-40.png)

![2025-05-21_04-40_1.png](Lab%20SQL%20injection%20UNION%20attack,%20retrieving%20multipl%201efc172892ad80b68981e3c238b720d8/2025-05-21_04-40_1.png)

### **Community solutions**

> [https://youtu.be/lu_8CT0JwZs](https://youtu.be/lu_8CT0JwZs)
>