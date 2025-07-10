# Lab 03: Username enumeration via response timing

🎯 **Lab Objective**

This lab is vulnerable to **username enumeration** using **response times** and uses **IP-based brute-force protection**.

Your goal:

- ✅ Identify a valid username
- ✅ Brute-force the user's password
- ✅ Log in and access the user account page

---

### 🧾 Credentials Provided

- 👤 Username: `wiener`
- 🔐 Password: `peter`

### 🧰 Resources

- 📄 **Candidate Usernames**
- 📄 **Candidate Passwords**

---

## 🚀 Step-by-Step Solution

### 🔐 Step 1: Initial Request and Block Detection

1. Submit an **invalid username & password**.
2. Intercept the `POST /login` request and send it to **Burp Repeater**.
3. Try multiple combinations and observe:
    - 🔥 **Your IP gets blocked** after too many invalid attempts.

---

### 💡 Step 2: Bypass IP Blocking

1. Add the `X-Forwarded-For` header:
    
    ```
    X-Forwarded-For: 192.168.1.X
    
    ```
    
2. Confirm that **spoofing this header bypasses** the block. ✅

---

### ⏱️ Step 3: Response Time-Based Username Enumeration

1. Use **your own valid username** (`wiener`) and test with:
    - 🔐 Short vs long password values
2. Observe:
    - ❌ **Invalid usernames**: fast response
    - ✅ **Valid username**: response slows with password length

---

### 🔁 Step 4: Burp Intruder Attack (Pitchfork)

1. Send the same request to **Burp Intruder**
2. Set **Attack Type**: 🎯 **Pitchfork**
3. Add payload positions for:
    - `X-Forwarded-For`
    - `username`
4. Set the `password` to a long dummy string (e.g., `A...A` 100 characters)

### 🔧 Payload Configuration:

- **Payload Position 1** (ss):
    - Type: Numbers
    - From: `1` → `100`
    - Step: `1`
    - Max fraction digits: `0`
- **Payload Position 2** (`username`):
    - Paste your **candidate usernames**

🟢 Start the attack.

---

### 📊 Step 5: Analyze Results

1. Click **Columns → Response Received / Response Completed**
2. Find:
    - 🕒 A **notably longer response time**
3. 💡 **Repeat the slow one** to confirm — this is the **valid username**
    
    ✍️ *Note it down*
    

---

### 🧨 Step 6: Brute-force Password

1. Start a **new Intruder attack**
2. Add `X-Forwarded-For` again and make it a payload position
3. Use the **valid username** found above
4. Set payload position on the `password`

### 🔧 Payloads:

- **Position 1**: Add numbers (to vary IP spoofing)
- **Position 2**: Add your list of **candidate passwords**

▶️ **Start attack**

---

### 🔓 Step 7: Identify the Successful Login

- Look for a response with:
    
    ```
    HTTP Status: 302
    
    ```
    
- This indicates a **successful login** 🎉
    
    ✍️ *Note the matching password*
    

---

### ✅ Step 8: Solve the Lab

Use the credentials you found:

```
👤 Username: valid-username
🔐 Password: valid-password

```

➡️ Login and access the user account page to solve the lab!

---

## 🎬 Community Solution

📺 Watch the walkthrough:

👉 [https://youtu.be/Non_U2tGG6o](https://youtu.be/Non_U2tGG6o)