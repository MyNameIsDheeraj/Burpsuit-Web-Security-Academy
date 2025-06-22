# 05. Subverting application logic

### 🔐Scenario

Imagine an application that lets users log in with a **username** and **password**.

When a user submits the username `wiener` and the password `bluecheese`, the application performs the following SQL query:

```sql
SELECT * FROM users WHERE username = 'wiener' AND password = 'bluecheese'

```

---

### How it works:

- ✅ If the query returns a user’s details, **login is successful**.
- ❌ Otherwise, the login is **rejected**.

---

### Vulnerability: SQL Injection to Bypass Password Check

An attacker can log in as **any user** without knowing the password by exploiting SQL injection.

---

### Attack Example

- The attacker submits the username:

```sql
administrator'--
```

- The password field is left **blank**.

---

### Resulting SQL query:

```sql
SELECT * FROM users WHERE username = 'administrator'--' AND password = ''
```

---

### Explanation:

- The SQL comment sequence `-` causes the rest of the query to be ignored.
- The password check (`AND password = ''`) is **removed** from the query.
- The query effectively becomes:

```sql
SELECT * FROM users WHERE username = 'administrator'
```

- This returns the `administrator` user’s record.
- ✅ The attacker is **successfully logged in as the administrator**, bypassing the password check entirely.

---

> ⚠️ **Important**:
> 
> 
> This illustrates how SQL injection can lead to **unauthorized access** and complete compromise of user accounts.
> 

---