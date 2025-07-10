# Lab 05: 2FA simple bypass

> Scenario:
> 
> 
> This lab's **two-factor authentication** can be bypassed.
> 
> You already have a valid **username and password**, but **do not** have access to the user's **2FA verification code**.
> 

🎯 **Goal**: Access Carlos's account page to solve the lab.

---

### 👤 Credentials

- **Your account**: `wiener : peter`
- **Victim’s account**: `carlos : montoya`

---

### 🛠️ Solution Steps

1. ✅ **Log in** to your **own account**.
    - A **2FA verification code** will be sent to you via email.
    - 📧 Click the **Email client** button to check your messages.
        
        ![2025-07-10_12-41.png](LabImg/2025-07-10_12-41.png)
        
        ![2025-07-10_12-42.png](LabImg/2025-07-10_12-42.png)
        
        ![2025-07-10_12-43.png](LabImg/2025-07-10_12-43.png)
        
        ![2025-07-10_12-43_1.png](LabImg/2025-07-10_12-43_1.png)
        
2. 🔎 Go to your **account page** and **note the URL**.
    - It will typically be something like:
        
        `/my-account`
        
3. 🔒 **Log out** of your account.
4. 🔑 **Log in using the victim’s credentials**:
    
    `carlos : montoya`
    
    ![2025-07-10_12-45.png](LabImg/2025-07-10_12-45.png)
    
5. 🚫 When prompted for the **verification code**, **do not enter anything**.
6. ✏️ Instead, **manually change the URL** in the browser to navigate directly to:
    
    ```
    /my-account
    ```
    
    ![2025-07-10_12-47.png](LabImg/2025-07-10_12-47.png)
    
7. 🎉 If the page loads, the lab is solved!
    
    ![2025-07-10_12-47_1.png](LabImg/2025-07-10_12-47_1.png)
    

---

### 📺 Community Solutions

🔗 [Watch on YouTube](https://youtu.be/2WpBVanEn3M)