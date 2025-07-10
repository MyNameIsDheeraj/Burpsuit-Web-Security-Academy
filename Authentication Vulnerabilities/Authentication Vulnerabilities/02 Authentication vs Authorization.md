# 02. Authentication vs. Authorization

Understanding the difference between **authentication** and **authorization** is crucial for building and maintaining **secure web applications**.

---

### ✅ **Authentication**

> Definition: Authentication is the process of verifying that a user is who they claim to be.
> 

👤 **Example**:

Authentication determines whether someone attempting to access a website with the username `Carlos123` **really is** the same person who created the account.

🔍 **Purpose**:

To confirm the **identity** of the user.

---

### 🛂 **Authorization**

> Definition: Authorization involves verifying whether a user is allowed to do something.
> 

🔐 **Example**:

Once `Carlos123` is authenticated, their permissions determine what they are **authorized** to do.

For example:

- Access personal information about other users
- Perform actions such as **deleting another user's account**

🎯 **Purpose**:

To control **access and privileges** within the application after identity is confirmed.

---

### 🧩 **Quick Summary**

| Aspect | Authentication 🔐 | Authorization 🛂 |
| --- | --- | --- |
| **Purpose** | Who you are | What you can do |
| **Happens when?** | First, before authorization | After authentication |
| **Example** | Login with username & password | Access admin panel |