# Lab 11: Password brute-force via password change

🚨 **Vulnerability:** The password change functionality can be exploited to **brute-force the victim’s password**.

🎯 **Goal:** Use the provided list of candidate passwords to brute-force **Carlos’s** account and access his **"My account"** page.

---

### 🛠️ **Your Credentials:**

- Username: `wiener`
- Password: `peter`

👤 **Victim’s Username:** `carlos`

📜 [**Candidate Passwords**](https://portswigger.net/web-security/authentication/auth-lab-passwords)

---

## 📝 **Solution Steps:**

1️⃣ **Start Burp Suite** and log in to your account.

- Experiment with the **password change functionality**.
- Observe that the **username** is sent as **hidden input** in the request form.

![2025-08-13_15-52.png](LabImg/2025-08-13_15-52.png)

![2025-08-13_15-53.png](LabImg/2025-08-13_15-53.png)

2️⃣ Notice the behavior when entering the **wrong current password**:

- If the **two entries for the new password match** → Account is **locked** 🔒
- If you enter **two different new passwords** → Error: `"Current password is incorrect"`
- If you enter a **valid current password** but two different new passwords → Error: `"New passwords do not match"`

💡 This last message can be used to **enumerate correct passwords** ✅

![2025-08-13_15-55.png](LabImg/2025-08-13_15-55.png)

![2025-08-13_15-55_1.png](LabImg/2025-08-13_15-55_1.png)

![2025-08-13_15-56.png](LabImg/2025-08-13_15-56.png)

![2025-08-13_15-58.png](LabImg/2025-08-13_15-58.png)

![2025-08-13_15-58_1.png](LabImg/2025-08-13_15-58_1.png)

3️⃣ Enter **your correct current password** and **two different new passwords**.

- Send this `POST /my-account/change-password` request to **Burp Intruder**.

![2025-08-13_16-00.png](LabImg/2025-08-13_16-00.png)

4️⃣ In **Burp Intruder**:

- Change the `username` parameter to `carlos`
- Add a payload position around the `current-password` parameter.
- Ensure the two new password fields are **different**. Example:
    
    ```
    username=carlos&current-password=§incorrect-password§&new-password-1=123&new-password-2=abc
    ```
    

![2025-08-13_16-02.png](LabImg/2025-08-13_16-02.png)

![2025-08-13_16-04.png](LabImg/2025-08-13_16-04.png)

![2025-08-13_16-05.png](LabImg/2025-08-13_16-05.png)

5️⃣ In the **Payloads** panel:

- Enter the list of candidate passwords as the payload set 📋

![2025-08-13_16-06.png](LabImg/2025-08-13_16-06.png)

6️⃣ In the **Settings** panel:

- Add a **Grep Match rule** to flag responses containing:
    
    ```
    New passwords do not match
    ```
    
- Start the attack 🚀

7️⃣ When the attack finishes:

- Identify the password that triggered the `"New passwords do not match"` message.
- This is **Carlos’s correct password** 🗝️

![2025-08-13_16-07.png](LabImg/2025-08-13_16-07.png)

8️⃣ In your browser:

- Log out of your account 🔓
- Log in with:
    - Username: `carlos`
    - Password: *(identified password)*

9️⃣ Click **My account** to solve the lab ✅

![2025-08-13_16-08.png](LabImg/2025-08-13_16-08.png)

---

### 🎥 **Community Walkthrough:**

> [Watch the solution](https://youtu.be/tiIg6mGiTKI)
>