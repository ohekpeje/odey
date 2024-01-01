---
title: "Lab: Password reset broken logic"
datePublished: Mon Jan 01 2024 22:00:12 GMT+0000 (Coordinated Universal Time)
cuid: clqvgrvom000008jvcswr2r1n
slug: lab-password-reset-broken-logic
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1703967068106/87919279-1cc0-46b6-a212-5875f2b2fe68.png
tags: cybersecurity-1, websecurity, burpsuite, portswigger, handson, password-reset, hands-on-labs

---

**Introduction:** In the realm of web security testing, understanding vulnerabilities in password reset functionality is paramount. In this article, we will dissect a lab that exposes a broken logic scenario, showcasing the importance of robust password reset mechanisms.

**Lab Overview: Password Reset Broken Logic**

**Step 1: Initiate the Password Reset** With Burp Suite running, begin by clicking the "Forgot your password?" link. Enter your own username and click the "Email client" button to access the password reset email.

**Step 2: Reset Your Password** Within the email, click the provided link to reset your password. Set the new password to your preference.

**Step 3: Study Requests and Responses** In Burp Suite, navigate to Proxy &gt; HTTP history to study the requests and responses for the password reset functionality. Observe that the reset token is included as a URL query parameter in the reset email. Note that when submitting the new password, the `POST /forgot-password?temp-forgot-password-token` request contains the username as a hidden input. Send this request to Burp Repeater for further analysis.

**Step 4: Confirm Lack of Token Verification** In Burp Repeater, notice that the password reset functionality still works even if you delete the value of the `temp-forgot-password-token` parameter in both the URL and request body. This confirms that the token is not being checked during the submission of the new password.

**Step 5: Perform Token Manipulation** In the browser, request a new password reset and change your password again. Send the `POST /forgot-password?temp-forgot-password-token` request to Burp Repeater once more.

In Burp Repeater, delete the value of the `temp-forgot-password-token` parameter in both the URL and request body. Change the `username` parameter to "carlos," set the new password to your preference, and send the request.

**Step 6: Log in as Carlos** In the browser, log in to Carlos's account using the new password you just set. Click on "My account" to successfully solve the lab.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704049278733/405b627d-3aa7-49f9-a834-c80fb8c4755f.jpeg align="center")

**Conclusion:** This lab exercise sheds light on a broken logic scenario in password reset functionality. By following these steps, security enthusiasts gain practical experience in identifying and exploiting vulnerabilities in the password reset process. It is crucial to approach such exercises responsibly, emphasizing the importance of robust security measures in web applications.

Security professionals can leverage this knowledge to fortify password reset mechanisms, ensuring that such critical functionalities adhere to best practices. As the digital landscape evolves, understanding and addressing vulnerabilities become paramount in maintaining a secure online environment.

**Reference:**

[Lab: Password reset broken logic | Web Security Academy (portswigger.net)](https://portswigger.net/web-security/authentication/other-mechanisms/lab-password-reset-broken-logic)