---
title: "Lab: SQL injection with filter bypass via XML encoding"
datePublished: Tue Jan 23 2024 14:49:27 GMT+0000 (Coordinated Universal Time)
cuid: clrqh2nli000709l14mi76je0
slug: lab-sql-injection-with-filter-bypass-via-xml-encoding
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1704889657477/7a05f880-bd67-4f0f-91f5-16347cfffa84.png
tags: cybersecurity-1, websecurity, burpsuite, sqlinjection, sqli, portswigger, handson

---

Lab Scenario: Our mission is to explore and exploit a web application's SQL injection vulnerability while overcoming a Web Application Firewall (WAF) by leveraging XML encoding. By manipulating the XML-formatted requests, we intend to bypass security filters and retrieve sensitive data from the database. Let's embark on this educational journey using Burp Suite:

1. **Identifying the Vulnerability:**
    
    * Observe that the stock check feature sends the `productId` and `storeId` to the application in XML format.
        
    * Send the `POST /product/stock` request to Burp Repeater.
        
    * In Burp Repeater, probe the `storeId` to check if input is evaluated, using expressions like `<storeId>1+1</storeId>`.
        
2. **Probing for Columns and WAF Bypass:**
    
    * Attempt to determine the number of columns returned by the original query using a UNION SELECT statement.
        
        ```plaintext
        xmlCopy code<storeId>1 UNION SELECT NULL</storeId>
        ```
        
    * Note that the request has been blocked due to WAF detection.
        
    * Bypass the WAF by obfuscating your payload using XML entities with tools like the **Hackvertor** extension.
        
3. **Crafting the Exploit:**
    
    * Deduce that the query returns a single column.
        
    * Concatenate returned usernames and passwords using SQL injection:
        
        ```plaintext
        <storeId><@hex_entities>1 UNION SELECT username || '~' || password FROM users<@/hex_entities></storeId>
        ```
        
    * Observe that you've successfully fetched usernames and passwords from the database, separated by a ~ character.
        
4. **Solving the Lab:**
    
    * Use the administrator's credentials obtained from the exploit to log in and solve the lab.
        

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704535793237/a112e14f-f5a1-4e96-8c81-b86d711b27a6.png align="left")

**Conclusion**: This hands-on lab exercise provides practical insights into exploiting SQL injection vulnerabilities with filter bypass using XML encoding. By following this step-by-step guide, users can enhance their understanding of advanced SQL injection techniques and the importance of secure coding practices. Stay informed, keep learning, and continue exploring the dynamic field of cybersecurity to contribute to a more secure online environment.

**Reference**:

[https://portswigger.net/web-security/sql-injection/lab-sql-injection-with-filter-bypass-via-xml-encoding](https://portswigger.net/web-security/sql-injection/lab-sql-injection-with-filter-bypass-via-xml-encoding)