# 2. What is the impact of a CSRF attack?

### 🎯 Goal of the attacker:

Trick a logged-in user into changing their email address on a trusted website (like `myaccount.com`) without their permission.

---

### 🧍‍♂️ The victim:

- Logged in to `myaccount.com`
- Has access to change their account details, including their email address

---

### 🪝 What happens:

1. The victim logs in to `myaccount.com` — they now have a valid **session cookie** stored in their browser.
2. They visit the attacker’s website while still logged in.
3. The attacker’s page **auto-submits** the form to `myaccount.com/change-email`.
4. The browser **includes the session cookie**, because it still trusts `myaccount.com`.
5. The server thinks the user wanted to change their email to `attacker@example.com`.

💥 The email address is now changed without the victim knowing!

---

### 🔥 **Examples of Actions the Attacker Can Trigger:**

| Action Type | Example Attack | Potential Consequence |
| --- | --- | --- |
| **Account Update** | Change email to `attacker@example.com` | Attacker resets the password via email |
| **Password Change** | Submit form to change password | Attacker logs in directly as the user |
| **Funds Transfer** | Send money to attacker's account | Financial theft |
| **Admin Abuse** | Delete users or create new admin accounts | Full application compromise |

If the victim is **an admin or privileged user**, the consequences can be catastrophic — such as:

- Total data deletion
- Application-wide changes
- Leakage of sensitive user information

---

### 🛡️ **Defending Against CSRF:**

- **CSRF tokens**: Random tokens added to forms that attackers can't guess
- **Same Site cookies**: Prevent cookies from being sent with cross-site requests
- **Double-submit cookies**: Send the CSRF token in both a cookie and a form field
- **User confirmation steps**: Ask users to re-enter passwords for sensitive actions

The real site (`myaccount.com`) should:

- Use a **CSRF token** in the email change form
- Only allow the form to submit if the **token is valid**
- This way, an attacker **cannot guess or steal** the token

> Django will reject the request **if the CSRF token is missing or incorrect**.
>