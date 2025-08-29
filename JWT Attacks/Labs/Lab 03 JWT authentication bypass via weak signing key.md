# Lab 03: JWT authentication bypass via weak signing key

This lab uses a **JWT-based mechanism** 🪪 for handling sessions.

It uses an **extremely weak secret key** 🔑 to sign and verify tokens, which can be **easily brute-forced** using a wordlist of common secrets 📜.

🎯 **Goal:**

1. Brute-force the website's secret key 🕵️‍♂️
2. Use it to sign a **modified session token** to access `/admin` 🛡
3. Delete the user **carlos** 🗑

---

### 🔑 Credentials

```
Username: wiener
Password: peter
```

💡 **Tip:**

- Learn how to work with **JWTs in Burp Suite** 🐞 before starting.
- Use **hashcat** 🐱‍💻 to brute-force the secret key (see *Brute-forcing secret keys using hashcat*).
    
    ![2025-08-17_22-05.png](Lab%2003%20JWT%20authentication%20bypass%20via%20weak%20signing%20%20250c172892ad8096a709cea2463d08bd/2025-08-17_22-05.png)
    

---

## 📝 Solution Steps

---

### 🥇 Part 1 - Brute-force the Secret Key

1️⃣ **Install Burp JWT Editor**

- Load the **JWT Editor** extension from the **BApp Store** 🛒.

2️⃣ **Log in and Capture the JWT**

- Log in to the lab using the given credentials ✅.
- Send the post-login **`GET /my-account`** request to **Burp Repeater** 📩.

3️⃣ **Test Admin Panel Access**

- In Burp Repeater, change the path to:

```
/admin
```

- Send the request 🚀.
- Observe that **only the administrator** 👑 can access it.

4️⃣ **Brute-force the Secret with Hashcat**

- Copy the JWT from your request 🪪.
- Run:

```bash
hashcat -a 0 -m 16500 <YOUR-JWT> /path/to/jwt.secrets.list
```

- If successful, hashcat will reveal:

```
<jwt>:secret1
```

✅ **Weak secret found:** `secret1`

📌 **Note:**

If you run the command again, use:

```
--show
```

to display results.

![2025-08-17_22-07.png](Lab%2003%20JWT%20authentication%20bypass%20via%20weak%20signing%20%20250c172892ad8096a709cea2463d08bd/2025-08-17_22-07.png)

![2025-08-17_22-07_1.png](Lab%2003%20JWT%20authentication%20bypass%20via%20weak%20signing%20%20250c172892ad8096a709cea2463d08bd/2025-08-17_22-07_1.png)

![2025-08-17_22-10.png](Lab%2003%20JWT%20authentication%20bypass%20via%20weak%20signing%20%20250c172892ad8096a709cea2463d08bd/2025-08-17_22-10.png)

![2025-08-17_22-10_1.png](Lab%2003%20JWT%20authentication%20bypass%20via%20weak%20signing%20%20250c172892ad8096a709cea2463d08bd/2025-08-17_22-10_1.png)

---

### 🥈 Part 2 - Generate a Forged Signing Key

1️⃣ **Base64 Encode the Secret**

- In **Burp Decoder**, Base64 encode `secret1` → `c2VjcmV0MQ==`

2️⃣ **Create New Symmetric Key in Burp**

- Go to **JWT Editor → Keys tab** 🗝
- Click **New Symmetric Key** → **Generate** 🔄
- Replace the `k` property with the **Base64-encoded secret**.
- Click **OK** to save the key.

---

### 🥉 Part 3 - Modify and Sign the JWT

1️⃣ **Edit the JWT Payload**

- In Burp Repeater, open the `/admin` request.
- Switch to the **JSON Web Token editor tab**.
- Change:

```
sub: "wiener" → "administrator"
```

2️⃣ **Sign the Modified JWT**

- Click **Sign** at the bottom.
- Select the key you generated earlier.
- Ensure **"Don't modify header"** is checked ✅.
- Click **OK** — the token is now signed with the correct signature.

3️⃣ **Access the Admin Panel**

- Send the modified request 📤.
- Observe that you now have access 🏆.

4️⃣ **Delete Carlos**

- In the response, find:

```
/admin/delete?username=carlos
```

- Send the request 🗑 → **Lab Solved!** 🎉
    
    ![2025-08-29_01-53.png](Lab%2003%20JWT%20authentication%20bypass%20via%20weak%20signing%20%20250c172892ad8096a709cea2463d08bd/2025-08-29_01-53.png)
    
    ![2025-08-29_01-54.png](Lab%2003%20JWT%20authentication%20bypass%20via%20weak%20signing%20%20250c172892ad8096a709cea2463d08bd/2025-08-29_01-54.png)
    
    ![2025-08-29_01-55.png](Lab%2003%20JWT%20authentication%20bypass%20via%20weak%20signing%20%20250c172892ad8096a709cea2463d08bd/2025-08-29_01-55.png)
    
    ![2025-08-29_01-55_1.png](Lab%2003%20JWT%20authentication%20bypass%20via%20weak%20signing%20%20250c172892ad8096a709cea2463d08bd/2025-08-29_01-55_1.png)
    
    ![2025-08-29_01-55_2.png](Lab%2003%20JWT%20authentication%20bypass%20via%20weak%20signing%20%20250c172892ad8096a709cea2463d08bd/2025-08-29_01-55_2.png)
    
    ![2025-08-29_01-56.png](Lab%2003%20JWT%20authentication%20bypass%20via%20weak%20signing%20%20250c172892ad8096a709cea2463d08bd/2025-08-29_01-56.png)
    

---

## 📹 Community Solutions

🎥 Watch here → [YouTube Solution](https://youtu.be/ov9yT4WAuzI)