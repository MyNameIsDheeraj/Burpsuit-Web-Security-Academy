# 02. How to detect SQL injection vulnerabilities

To detect SQL injection vulnerabilities, you can perform a **systematic set of tests** on every input or entry point in the application by submitting various payloads and analyzing responses:

---

## 💪Common Manual Tests:

- **Submit a single quote `'`**
    
    Watch for errors or unusual behavior indicating improper input handling.
    
- **Send SQL-specific syntax** that evaluates to:
    - The **base/original value** of the input, and
    - A **different value**
        
        Compare responses for systematic differences.
        
- **Try Boolean conditions**, such as:
    - `OR 1=1` (always true)
    - `OR 1=2` (always false)
        
        Observe if the application responses differ, indicating SQL logic manipulation.
        
- **Use payloads that cause time delays** when executed in SQL queries
    
    Check if the response time changes, which can reveal blind SQL injection.
    
- **Send OAST payloads (Out-of-band Application Security Testing)**
    
    These payloads trigger network interactions outside the usual request-response cycle; monitor for any unexpected network activity.
    

---

## ⚡ Faster Alternative: Use Burp Scanner

For quicker and more reliable detection of most SQL injection vulnerabilities, you can use **Burp Suite’s automated Scanner**. It automates these tests and highlights vulnerable points efficiently.