---
title: "Lab: SQL injection vulnerability allowing login bypass"
datePublished: Mon Jan 15 2024 11:46:51 GMT+0000 (Coordinated Universal Time)
cuid: clrev10oy000d09k0fp4o7dnq
slug: lab-sql-injection-vulnerability-allowing-login-bypass
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1704889727993/4fd394d9-674a-41e4-b7bf-5e419f052b4f.png
tags: cybersecurity-1, websecurity, burpsuite, sqlinjection, portswigger, handson

---

Lab Scenario: Our objective is to explore and exploit a web application's SQL injection vulnerability, allowing us to bypass the login process. By intercepting and modifying the login request, we aim to manipulate the SQL query to gain unauthorized access to the targeted account. Let's embark on this journey using Burp Suite:

1. **Intercepting the Login Request:**
    
    * Use Burp Suite to intercept and modify the login request.
        
    * Identify the parameter susceptible to SQL injection, in this case, the `username` parameter.
        
2. **Modifying the Parameter:**
    
    * Modify the `username` parameter by injecting the value `administrator'--`.
        
    * This payload is designed to manipulate the SQL query by commenting out the rest of the query after the injected payload.
        
    * Observe that the modified request looks like this:
        
        ```plaintext
        makefileCopy codeusername=administrator'--
        ```
        
3. **Sending the Modified Request:**
    
    * Forward the modified request and observe the response from the server.
        
    * Note that the response indicates a successful login, demonstrating the successful exploitation of the SQL injection vulnerability.
        
4. **Accessing the Account:**
    
    * Log in with the manipulated credentials to access the targeted account and successfully bypass the login mechanism.
        

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704534662437/443e7239-cb0d-4c7c-8f81-3a4211f97be6.png align="left")

**Conclusion:** This lab exercise provides hands-on experience in exploiting a SQL injection vulnerability to bypass login mechanisms, showcasing the potential risks associated with inadequate security measures. By following this step-by-step guide, users can enhance their skills in identifying, exploiting, and mitigating SQL injection flaws. Stay informed, keep learning, and continue exploring the dynamic field of cybersecurity to contribute to a more secure online environment.

**Reference**:

[https://portswigger.net/web-security/sql-injection/lab-login-bypass](https://portswigger.net/web-security/sql-injection/lab-login-bypass)