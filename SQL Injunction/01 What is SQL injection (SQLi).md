# 01. What is SQL injection (SQLi)?

**SQL injection (SQLi)** is a web security vulnerability that allows an attacker to **interfere with the queries** that an application makes to its database.

---

## ⚠️ What Can an Attacker Do?

- **View data** they are normally **not authorized to access**, such as:
    - Data belonging to other users
    - Any other data accessible by the application
- **Modify or delete data**, causing:
    - Persistent changes to the application’s content or behavior

---

## 🔥 Potential Impact

In some situations, a SQL injection attack can escalate to:

- **Compromise the underlying server** or other back-end infrastructure
- **Perform denial-of-service (DoS) attacks**