# 14. Bypassing SameSite cookie restrictions

### 📌 **What is SameSite?**

The `SameSite` attribute is a **browser security mechanism** that controls whether a website’s cookies are sent along with requests initiated from other origins. It helps mitigate various cross-site vulnerabilities, such as:

- **Cross-Site Request Forgery (CSRF)**
- **Cross-site information leaks**
- **Certain Cross-Origin Resource Sharing (CORS) exploits**

---

### 🌐 **Modern Browser Behavior**

Since **2021**, **Google Chrome** enforces `SameSite=Lax` **by default** on cookies that **do not specify** a `SameSite` value. This approach is part of a broader standardization effort, and it's anticipated that **other major browsers** will follow suit.

---

### 🧠 **Why This Matters**

Due to this change, understanding how `SameSite` restrictions work—and how they can be **bypassed**—is **critical** for web security testing. A site that appears protected might still be vulnerable if these mechanisms are not implemented correctly.

---

### 🗺️ **What You'll Learn**

In this section, we will:

- Explain the **functionality** and types of the `SameSite` attribute.
- Clarify **key terminology** related to cookie handling and browser request contexts.
- Explore **bypass techniques** for defeating SameSite restrictions.
- Demonstrate **real-world scenarios** where cross-site attacks may still succeed.

---