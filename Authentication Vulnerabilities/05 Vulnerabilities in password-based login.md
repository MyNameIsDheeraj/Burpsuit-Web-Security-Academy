# 05. Vulnerabilities in password-based login

## 🔐 Password-Based Authentication & Vulnerabilities

For websites that adopt a **password-based login process**, users either register for an account themselves or are assigned one by an administrator. This account is associated with:

- ✍️ A **unique username**
- 🔑 A **secret password**

This is entered into a **login form** to authenticate themselves.

> The fact that they know the secret password is taken as sufficient proof of identity.
> 

🚨 If an attacker obtains or guesses these credentials, the **security of the website is compromised**.

---

## 💥 Brute-force Attacks

A **brute-force attack** uses trial and error to guess valid credentials. These are typically automated using tools and **wordlists** of usernames and passwords.

⚙️ **Automating brute-force attacks** allows attackers to:

- Make thousands of login attempts per second
- Bypass weak login mechanisms quickly

💡 Attackers often enhance these with:

- Publicly available data
- Known username patterns
- Logic-based guesses

This makes the attack **far more efficient** than random guessing.

---

## 👤 Brute-forcing Usernames

Usernames are often predictable:

📧 **Patterns like** `firstname.lastname@company.com`

🔐 Common privileged accounts: `admin`, `administrator`

Also check:

- 📂 User profiles visible without login
- 📧 Email addresses in HTTP responses
- 🔍 Any disclosed usernames of high-privileged users

---

## 🔑 Brute-forcing Passwords

Password strength varies. Many sites enforce **password policies** requiring:

- ✅ Minimum length
- 🔠 Mixed case
- 🔣 Special characters

🧠 But users often:

- Use **easily remembered patterns**, like `Mypassword1!` or `Myp4$$w0rd`
- Make **predictable changes**, e.g. `Mypassword1!` → `Mypassword2!`

🧰 Attackers **use this behavior** to design more **effective brute-force dictionaries**.

---

## 🕵️‍♂️ Username Enumeration

Username enumeration allows attackers to **discover valid usernames** based on differences in responses.

### ⚠️ How to Detect Enumeration

- 📟 **Status Codes**
    
    Different codes (e.g. 401 vs 403) may indicate a valid username.
    
- 💬 **Error Messages**
    
    Varying messages like:
    
    - “Username not found” vs. “Incorrect password”
    - Even invisible typos can expose this
- ⏱️ **Response Times**
    
    Valid usernames might lead to **slightly longer processing** due to password checks.
    

> 🚨 These small differences allow attackers to compile shortlists of valid usernames, reducing brute-force time.
> 

---

## 📌 Summary

- 🔓 Weak login implementations are highly vulnerable to brute-force attacks.
- 🧠 Attackers exploit **human behavior** and **pattern predictability**.
- 🎯 Username enumeration can drastically reduce brute-force effort.
- 🔐 Websites should implement:
    - Rate limiting
    - Strong password policies
    - Uniform responses to authentication attempts