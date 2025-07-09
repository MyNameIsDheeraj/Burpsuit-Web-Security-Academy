# 04. Finding hidden parameters

When you're doing **API recon**, you may uncover **undocumented parameters** that the API supports.

> 🧠 You can try using these to change the application’s behavior.
> 

Burp Suite offers a variety of tools to help identify these hidden parameters. 🔍

---

### 🧨 **Burp Intruder**

📦 **What it does:**

- Automatically discovers **hidden parameters**
- Uses a **wordlist of common parameter names** to:
    - Replace existing parameters
    - Add new parameters

🧠 **Pro Tip:**

➤ Include **custom parameter names** relevant to the application, based on your **initial recon**.

---

### 🧱 **Param Miner (BApp)**

🧰 **What it does:**

- Automatically **guesses up to 65,536 parameter names** per request
- Leverages application context from **scope analysis**

🎯 **Smart guessing**:

➤ Uses names that are **relevant to the application**

---

### 🔎 **Content Discovery Tool**

📂 **Purpose:**

- Helps uncover **non-visible content** such as:
    - Unlinked pages
    - Hidden resources
    - 🧩 **Parameters** not exposed in the UI

> 🧭 This expands the attack surface for further testing and fuzzing.
>