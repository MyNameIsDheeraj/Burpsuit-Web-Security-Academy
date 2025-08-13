# 14. Preventing Attacks on Your Own Authentication Mechanisms

We’ve seen multiple ways authentication can be **vulnerable** due to poor implementation.

To **reduce risk**, follow these **key principles** when securing your own websites.

---

## 🔑 **Take Care with User Credentials**

Even the **strongest authentication** is useless if you **leak valid login credentials** 🕵️.

- ❌ Never send login data over **unencrypted connections**
- ✅ Use **HTTPS** for all login requests
- 🔄 Redirect all **HTTP requests** → **HTTPS**
- 🔍 Audit your site to ensure:
    - No usernames/emails are leaked in **public profiles**
    - No sensitive data is reflected in **HTTP responses**

---

## 🚫 **Don’t Count on Users for Security**

Human nature means users will **find shortcuts** to avoid extra effort 😅.

Enforce secure behavior where possible:

- 📏 Implement an **effective password policy**
- ❌ Avoid old-school policies that users bypass with predictable passwords
- 💡 Use a **real-time password strength checker** (e.g., Dropbox’s `zxcvbn`)
- 🛡️ Only accept passwords with **high strength ratings**

---

## 🙈 **Prevent Username Enumeration**

It’s easier for attackers to break authentication if they **know a username exists**.

- ❗ In some cases, just knowing someone has an account can be sensitive info
- 🔐 Use **identical, generic error messages** whether username exists or not
- 📄 Return the **same HTTP status code** for all login attempts
- ⏱️ Keep **response times consistent** in all scenarios

---

## 🛠️ **Implement Robust Brute-force Protection**

Brute-force attacks are **simple to execute**, so disrupt them:

- 🚫 **IP-based rate limiting**
- 🕵️ Prevent attackers from faking/changing their IP
- 🧩 Require **CAPTCHA** after repeated failed logins
- ⏳ Make attacks **slow and tedious** so attackers give up

---

## 🔍 **Triple-check Your Verification Logic**

Logic flaws in authentication can be **catastrophic**:

- 🧪 Audit **all verification/validation code** thoroughly
- ❌ A bypassable check is almost as bad as **no check at all**

---

## 📌 **Don’t Forget Supplementary Functionality**

Attackers may exploit **related authentication features**:

- 🔓 Password reset pages
- 🔑 Password change pages
- 🛠️ Registration flows
    
    These must be **just as secure** as the main login system.
    

---

## 🧾 **Implement Proper Multi-Factor Authentication (MFA)**

While MFA isn’t always practical, **when done right** it greatly improves security:

- ❌ Verifying multiple instances of the **same factor** is **not true MFA**
- 📧 Email verification codes = single-factor (just slower)
- 📱 SMS 2FA = better, but can be abused (e.g., SIM swapping)
- ✅ **Best:** Use a **dedicated device or authenticator app** (generates codes offline)
- 🔄 Just like main auth logic, **ensure MFA checks can’t be bypassed**