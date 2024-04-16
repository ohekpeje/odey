---
title: "Lab: Exploiting XInclude to retrieve files"
datePublished: Tue Apr 16 2024 05:48:23 GMT+0000 (Coordinated Universal Time)
cuid: clv1yqegk000308jr52rc0pl6
slug: lab-exploiting-xinclude-to-retrieve-files
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1704888789347/a77f6972-1ae5-4889-abf2-d998a9055fd8.png
tags: cybersecurity-1, websecurity, burpsuite, xxe, portswigger, handson

---

Lab Scenario: Our mission is to exploit XInclude through a web application's "Check stock" feature. By intercepting and manipulating a POST request, we intend to use XInclude to retrieve files from the server. Let's proceed with the solution:

1. **Intercepting the POST Request:**
    
    * Visit a product page and click "Check stock."
        
    * Intercept the resulting POST request using Burp Suite.
        
2. **Manipulating the productId Parameter:**
    
    * Set the value of the `productId` parameter to exploit XInclude. Use the following payload:
        
        ```plaintext
        xmlCopy code<foo xmlns:xi="http://www.w3.org/2001/XInclude"><xi:include parse="text" href="file:///etc/passwd"/></foo>
        ```
        
        This payload uses XInclude to include the contents of the `/etc/passwd` file.
        
3. **Sending the Modified Request:**
    
    * Forward the modified request and observe the response from the server.
        
    * Note that the response contains the contents of the specified file, in this case, `/etc/passwd`.
        
4. **Exploiting XInclude for File Retrieval:**
    
    * By utilizing XInclude, we have successfully retrieved the contents of a server file.
        
5. **Submitting the Solution:**
    
    * Use the appropriate method provided by the lab to submit the solution, confirming the successful retrieval of sensitive information.
        

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704540682594/554ee836-75c2-4043-bd1b-6b61a2742271.png align="left")

**Conclusion:** This lab exercise provides hands-on experience in exploiting XInclude to retrieve files from a web application. By following this step-by-step guide, users can deepen their understanding of XInclude vulnerabilities and the potential risks associated with improper handling of XML input. Stay informed, keep learning, and continue exploring the dynamic field of cybersecurity to contribute to a more secure online environment.

**Reference**:

[https://portswigger.net/web-security/xxe](https://portswigger.net/web-security/xxe)

[https://portswigger.net/web-security/xxe/lab-xinclude-attack](https://portswigger.net/web-security/xxe/lab-xinclude-attack)