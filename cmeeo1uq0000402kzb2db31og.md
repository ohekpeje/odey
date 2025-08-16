---
title: "Lab: HTTP/2 request splitting via CRLF injection"
datePublished: Sat Aug 16 2025 19:44:46 GMT+0000 (Coordinated Universal Time)
cuid: cmeeo1uq0000402kzb2db31og
slug: lab-http2-request-splitting-via-crlf-injection
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1704888424223/578a1ede-6982-4370-9d3c-d2feaeda3d5d.png
tags: http2, crlf, websecurity, burpsuite, injection, portswigger, request-smuggling

---

Our target is to exploit a hypothetical web application, simulating real-world scenarios. To demonstrate HTTP/2 request splitting, we will follow a step-by-step solution provided by the lab:

1. **Setup with Burp Suite:** Start by sending a request for `GET /` to Burp Repeater. Expand the Inspector's Request Attributes section and set the protocol to HTTP/2.
    
2. **Poisoning the Response Queue:** Change the path of the request to a non-existent endpoint, e.g., `/x`, ensuring a consistent 404 response. This step poisons the response queue, making it easier to recognize captured responses.
    
3. **CRLF Injection:** Using the Inspector, append an arbitrary header with injected `\r\n` sequences to split the request, smuggling another request to a non-existent endpoint.
    
    ```plaintext
    Name: foo
    Value: bar\r\n\r\nGET /x HTTP/1.1\r\nHost: YOUR-LAB-ID.web-security-academy.net
    ```
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704553482006/2681e6ef-13e8-406b-be29-0eb7f22bc10a.png align="left")
    
4. **Exploiting Downgrading:** Send the request. The front-end server appends `\r\n\r\n` during downgrading, converting the smuggled prefix into a complete request, thus poisoning the response queue.
    
5. **Capturing Admin's Session Cookie:** Wait for about 5 seconds and resend the request to fetch an arbitrary response. Capture a 302 response containing the admin's post-login session cookie. ***If not successful, send 10 ordinary requests to reset the connection from repeater and try again.***
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704553702286/d3a84a3e-ae4f-4537-b0e1-fbbc0c712071.png align="left")
    
    Turn on intercept before accessing the host url as ***/admin*** so it can be captured in burp. This should capture the below image. Then send to repeater and replace session in repeater with session gotten from the 302. Turn off intercept after sending captured /admin request to repeater.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704554334354/53a8d984-4a26-4118-ad5b-8aee0925c4fe.png align="left")
    
6. **Accessing Admin Panel:** Copy the session cookie obtained and use it to send a GET request to `/admin`. Repeat until you receive a 200 response containing the admin panel.
    
7. **Deleting 'Carlos' to Solve the Lab:** In the admin panel response, find the URL for deleting 'carlos' (`/admin/delete?username=carlos`). Update the path in your request accordingly and send the request to solve the lab.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704553457429/09d37bf6-d8ce-4cb4-8d51-c299843acd0c.png align="left")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704557373741/88fcd1d9-8840-489e-a9f8-ffb08552e727.png align="center")

**Conclusion**: HTTP/2 request splitting via CRLF injection demonstrates the importance of understanding and addressing potential vulnerabilities in web applications. By following this step-by-step guide, users can enhance their knowledge of web security and contribute to creating a more robust online environment. Stay curious, keep learning, and continue exploring the dynamic field of cybersecurity.

**Reference**:

[https://portswigger.net/web-security/request-smuggling/advanced/lab-request-smuggling-h2-request-splitting-via-crlf-injection](https://portswigger.net/web-security/request-smuggling/advanced/lab-request-smuggling-h2-request-splitting-via-crlf-injection)