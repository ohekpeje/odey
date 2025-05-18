---
title: "Lab: OS command injection, simple case"
datePublished: Sun May 18 2025 20:17:58 GMT+0000 (Coordinated Universal Time)
cuid: cmau3lvsq000a09l5g96z8rbt
slug: lab-os-command-injection-simple-case
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1704889772637/1da482dd-8470-472f-8d82-25cc9064d2f2.png
tags: sqlinjection

---

Lab Scenario: Our objective is to explore and exploit an OS command injection vulnerability in a web application's stock level check feature. By intercepting and modifying a request, we aim to execute arbitrary commands and observe the response, highlighting the risks associated with such vulnerabilities. Let's embark on this journey using Burp Suite:

1. **Intercepting the Request:**
    
    * Use Burp Suite to intercept and modify a request that checks the stock level.
        
    * Identify the parameter susceptible to OS command injection, in this case, the `storeID` parameter.
        
2. **Modifying the Parameter:**
    
    * Modify the `storeID` parameter by injecting the value `1|whoami`. This payload is designed to execute the `whoami` command, revealing the name of the current user.
        
    * Observe that the modified request looks like this:
        
        ```plaintext
        storeID=1|whoami
        ```
        
3. **Observing the Response:**
    
    * Forward the modified request and observe the response from the server.
        
    * Note that the response contains the name of the current user, demonstrating the successful execution of the injected OS command.
        

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704974913761/aa2f675d-8d03-40ca-85c4-450e7360680c.jpeg align="center")

**Conclusion:** This simple lab exercise provides hands-on experience in exploiting an OS command injection vulnerability. By following this step-by-step guide, users can gain insights into the potential risks associated with command injection and the importance of securing web applications against such exploits. Stay informed, keep learning, and continue exploring the dynamic field of cybersecurity to contribute to a more secure online environment.

**Reference**:

[https://portswigger.net/web-security/os-command-injection/lab-simple](https://portswigger.net/web-security/os-command-injection/lab-simple)