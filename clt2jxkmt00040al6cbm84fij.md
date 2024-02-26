---
title: "Lab: SQL injection vulnerability in WHERE clause allowing retrieval of hidden data"
datePublished: Mon Feb 26 2024 06:22:25 GMT+0000 (Coordinated Universal Time)
cuid: clt2jxkmt00040al6cbm84fij
slug: lab-sql-injection-vulnerability-in-where-clause-allowing-retrieval-of-hidden-data
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1704889813113/a11a2287-f79f-46ee-a23f-fc93da97ee2b.png
tags: cybersecurity-1, websecurity, burpsuite, sqlinjection, sqli, portswigger, handson

---

Lab Scenario: Our objective is to understand and exploit a SQL injection vulnerability in the WHERE clause of a web application's stock check feature. By carefully probing and bypassing security measures, we aim to retrieve hidden data and ultimately solve the lab. Let's embark on this journey using Burp Suite:

1. **Identifying the Vulnerability:**
    
    * Observe that the stock check feature sends the `productId` and `storeId` to the application in XML format.
        
    * Send the `POST /product/stock` request to Burp Repeater.
        
2. **Probing for Injection Points:**
    
    * In Burp Repeater, probe the `storeId` to see if your input is evaluated. Try replacing the ID with mathematical expressions to evaluate other potential IDs:
        
        ```plaintext
        xmlCopy code<storeId>1+1</storeId>
        ```
        
    * Observe that your input appears to be evaluated, returning stock information for different stores.
        
3. **Bypassing the Web Application Firewall (WAF):**
    
    * Attempt to determine the number of columns returned by the original query using a UNION SELECT statement. Note that your request may be blocked.
        
        ```plaintext
        xmlCopy code<storeId>1 UNION SELECT NULL</storeId>
        ```
        
    * Bypass the WAF by obfuscating your payload using XML entities. Utilize tools like Hackvertor extension to encode entities.
        
    * Resend the request and confirm that you receive a normal response, indicating successful WAF bypass.
        
4. **Crafting the Exploit:**
    
    * Deduce that the query returns a single column. Attempting to return more than one column results in an error.
        
    * Concatenate the returned usernames and passwords using SQL injection:
        
        ```plaintext
        xmlCopy code<storeId><@hex_entities>1 UNION SELECT username || '~' || password FROM users<@/hex_entities></storeId>
        ```
        
    * Observe that you've successfully fetched usernames and passwords from the database, separated by a ~ character.
        
5. **Solving the Lab:**
    
    * Use the administrator's credentials obtained from the exploit to log in and solve the lab.
        

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704533870231/1f373c1d-804f-4011-a235-4ec1d863d675.png align="left")

**Conclusion**

This hands-on lab provides practical insights into exploiting SQL injection vulnerabilities in the WHERE clause, showcasing the potential risks associated with inadequate security measures. By following this step-by-step guide, users can enhance their skills in identifying, exploiting, and mitigating SQL injection flaws. Stay informed, keep learning, and continue exploring the dynamic field of cybersecurity to contribute to a more secure online environment.

**Reference**:

[https://portswigger.net/web-security/sql-injection](https://portswigger.net/web-security/sql-injection)

[https://portswigger.net/web-security/sql-injection/lab-sql-injection-with-filter-bypass-via-xml-encoding](https://portswigger.net/web-security/sql-injection/lab-sql-injection-with-filter-bypass-via-xml-encoding)