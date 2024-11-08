---
title: "Lab: Exploiting XXE to perform SSRF attacks"
datePublished: Fri Nov 08 2024 10:54:39 GMT+0000 (Coordinated Universal Time)
cuid: cm38mdr5e000409jsa15udjg5
slug: lab-exploiting-xxe-to-perform-ssrf-attacks
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1704888946874/17067007-ca6d-47e9-8b6f-18c97a084fb4.png
tags: cybersecurity-1, websecurity, burpsuite, xxe, portswigger, handson

---

Lab Scenario: Our mission is to exploit XXE through a web application's "Check stock" feature, ultimately performing SSRF attacks to access sensitive information from a metadata endpoint. By intercepting and manipulating a POST request, we intend to use XXE to trigger requests to a metadata endpoint and retrieve sensitive data. Let's proceed with the solution:

1. **Intercepting the POST Request:**
    
    * Visit a product page and click "Check stock."
        
    * Intercept the resulting POST request using Burp Suite.
        
2. **Inserting External Entity Definition:**
    
    * Insert the following external entity definition between the XML declaration and the `stockCheck` element:
        
        ```plaintext
        <!DOCTYPE test [ <!ENTITY xxe SYSTEM "http://169.254.169.254/latest/meta-data/iam/security-credentials/admin"> ]>
        ```
        
3. **Replacing the productId with External Entity Reference:**
    
    * Replace the `productId` number with a reference to the external entity: `&xxe;`.
        
    * The response should contain "Invalid product ID:" followed by the response from the metadata endpoint, initially a folder name.
        
4. **Iterative Exploration of the Metadata API:**
    
    * Iteratively update the URL in the Document Type Definition (DTD) to explore the API until reaching `/latest/meta-data/iam/security-credentials/admin`.
        
    * This should return JSON containing the `SecretAccessKey`.
        
5. **Confirming the Exploitation:**
    
    * Use the information obtained from the metadata endpoint to confirm the successful exploitation of SSRF through XXE.
        
6. **Submitting the Solution:**
    
    * Use the appropriate method provided by the lab to submit the solution, confirming the successful retrieval of sensitive information.
        

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704540010444/44ab17dd-ebae-48d3-a0d6-b85958f47ae4.png align="left")

**Conclusion:** This lab exercise provides practical insights into exploiting XXE vulnerabilities to perform SSRF attacks. By following this step-by-step guide, users can deepen their understanding of the relationship between XXE and SSRF, emphasizing the importance of securing against such vulnerabilities. Stay informed, keep learning, and continue exploring the dynamic field of cybersecurity to contribute to a more secure online environment.

**Reference**:

[https://portswigger.net/web-security/xxe](https://portswigger.net/web-security/xxe)

[https://portswigger.net/web-security/xxe/lab-exploiting-xxe-to-perform-ssrf](https://portswigger.net/web-security/xxe/lab-exploiting-xxe-to-perform-ssrf)