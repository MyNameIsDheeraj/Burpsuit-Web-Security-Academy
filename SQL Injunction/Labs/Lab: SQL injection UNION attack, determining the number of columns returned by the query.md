# Lab: SQL injection UNION attack, determining the number of columns returned by the query

This lab contains a SQL injection vulnerability in the product category filter. The results from the query are returned in the application's response, so you can use a UNION attack to retrieve data from other tables. The first step of such an attack is to determine the number of columns that are being returned by the query. You will then use this technique in subsequent labs to construct the full attack.

To solve the lab, determine the number of columns returned by the query by performing a SQL injection UNION attack that returns an additional row containing null values.

### **Solution**

1. Use Burp Suite to intercept and modify the request that sets the product category filter.

![2025-05-21_03-54.png](Lab_img/2025-05-21_03-54.png)

![2025-05-21_03-55.png](Lab_img/2025-05-21_03-55.png)

1. Modify the `category` parameter, giving it the value `'+UNION+SELECT+NULL--`. Observe that an error occurs.

![2025-05-21_03-56.png](Lab_img/2025-05-21_03-56.png)

1. `'+UNION+SELECT+NULL,NULL--`Modify the `category` parameter to add an additional column containing a null value:

![2025-05-21_03-59.png](Lab_img/2025-05-21_03-59.png)

1. Continue adding null values until the error disappears and the response includes additional content containing the null values.

![2025-05-21_04-00.png](Lab_img/2025-05-21_04-00.png)

![2025-05-21_04-00_1.png](Lab_img/2025-05-21_04-00_1.png)

### **Community solutions**

> [https://youtu.be/GP6CK03nDvw](https://youtu.be/GP6CK03nDvw)
>