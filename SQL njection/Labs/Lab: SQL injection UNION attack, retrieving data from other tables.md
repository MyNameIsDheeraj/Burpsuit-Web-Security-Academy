# Lab: SQL injection UNION attack, retrieving data from other tables

This lab contains a SQL injection vulnerability in the product category filter. The results from the query are returned in the application's response, so you can use a UNION attack to retrieve data from other tables. To construct such an attack, you need to combine some of the techniques you learned in previous labs.

The database contains a different table called `users`, with columns called `username` and `password`.

To solve the lab, perform a SQL injection UNION attack that retrieves all usernames and passwords, and use the information to log in as the `administrator` user.

### **Solution**

1. Use Burp Suite to intercept and modify the request that sets the product category filter.

![2025-05-21_04-24.png](Lab%20SQL%20injection%20UNION%20attack,%20retrieving%20data%20fr%201efc172892ad807881d9cd475edab070/2025-05-21_04-24.png)

![2025-05-21_04-24_1.png](Lab%20SQL%20injection%20UNION%20attack,%20retrieving%20data%20fr%201efc172892ad807881d9cd475edab070/2025-05-21_04-24_1.png)

1. `'+UNION+SELECT+'abc','def'--`Determine the number of columns that are being returned by the query and which columns contain text data. Verify that the query is returning two columns, both of which contain text, using a payload like the following in the category parameter:

![2025-05-21_04-25.png](Lab%20SQL%20injection%20UNION%20attack,%20retrieving%20data%20fr%201efc172892ad807881d9cd475edab070/2025-05-21_04-25.png)

1. `'+UNION+SELECT+username,+password+FROM+users--` Use the following payload to retrieve the contents of the `users` table:

![2025-05-21_04-27.png](Lab%20SQL%20injection%20UNION%20attack,%20retrieving%20data%20fr%201efc172892ad807881d9cd475edab070/2025-05-21_04-27.png)

![2025-05-21_04-27_1.png](Lab%20SQL%20injection%20UNION%20attack,%20retrieving%20data%20fr%201efc172892ad807881d9cd475edab070/2025-05-21_04-27_1.png)

1. Verify that the application's response contains usernames and passwords.

![2025-05-21_04-28.png](Lab%20SQL%20injection%20UNION%20attack,%20retrieving%20data%20fr%201efc172892ad807881d9cd475edab070/2025-05-21_04-28.png)

### **Community solutions**

> [https://youtu.be/ushDHoJbwEc](https://youtu.be/ushDHoJbwEc)
>