# 11. CSRF token is not tied to the user session

### 🔍 Description

Some applications **do not validate** that the CSRF token is tied to the **specific user session** making the request.

Instead, the application:

- Maintains a **global pool of issued tokens**.
- Accepts **any valid token** from that pool, regardless of which session it originated from.

---

### ⚠️ Security Implication

In this situation:

- An **attacker** can:
    - Log in to the application using **their own account**.
    - Obtain a **valid CSRF token** from their session.
    - Craft a CSRF attack using this token.
    - Deliver this crafted attack to a **victim user**.
- Because the application only checks whether the token is from the pool (and not tied to the session), it **accepts the attack**, allowing **unauthorized actions** on behalf of the victim.

---

### 🔓 Vulnerability Summary

| Parameter | Value |
| --- | --- |
| Type | CSRF token session misbinding |
| Token validation flaw | Token is not verified against the requesting user's session |
| Attack requirement | Attacker must obtain a token from their own session |
| Exploitable by | Delivering the token in a CSRF attack to a different (victim) session |