# Lab 02: JWT authentication bypass via flawed signature verification

This lab uses a **JWT-based mechanism** 🪪 for handling sessions.

The server is **insecurely configured** ⚠️ to **accept unsigned JWTs**.

🎯 **Goal:** Modify your session token to gain access to the **admin panel** at `/admin`, then delete the user **carlos** 🗑.

---

### 🔑 Credentials

```
Username: wiener
Password: peter
```

💡 **Tip:**

We recommend familiarizing yourself with **how to work with JWTs in Burp Suite** 🐞 before attempting this lab.

---

## 📝 Solution Steps

### 1️⃣ **Log in to your account**

Sign in with the provided credentials ✅.

---

### 2️⃣ **Inspect the JWT in Burp Suite**

- Go to **Proxy → HTTP history** 📜.
- Look at the **post-login `GET /my-account`** request.
- Observe that your **session cookie is a JWT** 🔍.
    
    ![2025-08-15_15-52.png](Lab%2002%20JWT%20authentication%20bypass%20via%20flawed%20signat%20250c172892ad80d99fbeea358f070a35/2025-08-15_15-52.png)
    
    ![2025-08-15_15-53.png](Lab%2002%20JWT%20authentication%20bypass%20via%20flawed%20signat%20250c172892ad80d99fbeea358f070a35/2025-08-15_15-53.png)
    

---

### 3️⃣ **View the JWT payload**

- Double-click the **payload** section of the token.
- In the **Inspector panel**, view the **decoded JSON** 📄.
- Notice that the `sub` claim contains your username 👤.
- Send this request to **Burp Repeater** 📩.

---

### 4️⃣ **Test admin panel access**

- Change the request path to:

```
/admin
```

- Send the request 🚀.
- Observe that **only the administrator** 👑 can access this panel.
    
    ![2025-08-15_15-56.png](Lab%2002%20JWT%20authentication%20bypass%20via%20flawed%20signat%20250c172892ad80d99fbeea358f070a35/2025-08-15_15-56.png)
    

---

### 5️⃣ **Modify the JWT payload**

- In the Inspector panel, change:

```
sub: "wiener" → "administrator"
```

- Click **Apply changes** 🖱.
    
    ![2025-08-15_15-57.png](Lab%2002%20JWT%20authentication%20bypass%20via%20flawed%20signat%20250c172892ad80d99fbeea358f070a35/2025-08-15_15-57.png)
    

---

### 6️⃣ **Bypass with alg=none**

- Select the **header** of the JWT.
- Change `alg` to:

```
none
```

- Click **Apply changes** ✏️.
    
    ![2025-08-15_15-57_1.png](Lab%2002%20JWT%20authentication%20bypass%20via%20flawed%20signat%20250c172892ad80d99fbeea358f070a35/2025-08-15_15-57_1.png)
    

---

### 7️⃣ **Remove the signature**

- In the message editor, delete the **signature part** of the JWT.
- **Important:** Leave the **trailing dot** (`.`) after the payload! ⚠️
    
    ![2025-08-15_16-00.png](Lab%2002%20JWT%20authentication%20bypass%20via%20flawed%20signat%20250c172892ad80d99fbeea358f070a35/2025-08-15_16-00.png)
    

---

### 8️⃣ **Access the admin panel**

- Send the modified request 📤.
- ✅ You have now successfully accessed the admin panel 🏆.
    
    ![2025-08-15_16-00_1.png](Lab%2002%20JWT%20authentication%20bypass%20via%20flawed%20signat%20250c172892ad80d99fbeea358f070a35/2025-08-15_16-00_1.png)
    

---

### 9️⃣ **Delete the user Carlos**

- In the **response**, find:

```
/admin/delete?username=carlos
```

- Send the request to this endpoint 🗑.
- 🎉 **Lab solved!**
    
    ![2025-08-15_16-00_2.png](Lab%2002%20JWT%20authentication%20bypass%20via%20flawed%20signat%20250c172892ad80d99fbeea358f070a35/2025-08-15_16-00_2.png)
    

---

## 📹 Community Solutions

🎥 Watch here → [YouTube Solution](https://youtu.be/rEUoU6OYH_g)