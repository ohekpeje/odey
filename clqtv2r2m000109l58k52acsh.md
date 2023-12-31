---
title: "Lab: Username enumeration via different responses"
datePublished: Sun Dec 31 2023 19:05:02 GMT+0000 (Coordinated Universal Time)
cuid: clqtv2r2m000109l58k52acsh
slug: lab-username-enumeration-via-different-responses
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1703965918417/39eff27f-9c62-4313-85f7-059bfc122cbd.png
tags: cybersecurity, websecurity, burpsuite, portswigger, handson, hands-on-labs

---

**Introduction:** When it comes to web application security testing, understanding the intricacies of Burp Suite and its various modules is crucial. In this article, we'll explore a step-by-step approach to password enumeration using Burp Intruder, a powerful feature of the Burp Suite toolkit.

**Step 1: Initial Investigation** With Burp Suite running, start by investigating the login page of the target application. Submit an invalid username and password to initiate the process.

**Step 2: Analyzing HTTP History** Navigate to Proxy &gt; HTTP history in Burp and locate the POST /login request. Highlight the value of the username parameter and send it to Burp Intruder.

**Step 3: Configuring Burp Intruder** Inside Burp Intruder, go to the Positions tab. Notice that the username parameter is automatically set as a payload position, indicated by two § symbols. Ensure the Sniper attack type is selected.

**Step 4: Payload Configuration** On the Payloads tab, select the Simple list payload type. Paste the list of candidate usernames under Payload settings. Click Start attack, and a new window will open.

**Step 5: Analyzing Results** After the attack is complete, examine the Results tab and sort by the Length column. Identify the entry with a longer response, indicating a potential successful login. Note the username in the Payload column.

**Step 6: Refining the Attack** Close the attack, return to the Positions tab, and clear the settings. Replace the username parameter with the identified username and add a payload position for the password parameter.

The updated payload configuration should look like this:

```plaintext
username=identified-user&password=§invalid-password§
```

On the Payloads tab, clear the list of usernames, replace it with the list of candidate passwords, and click Start attack.

**Step 7: Identifying Successful Login** After the attack, inspect the Status column. Look for a response with a 302 status code, indicating a successful login attempt. Note the password in the Payload column.

**Step 8: Logging In** Use the identified username and password to log in to the target application. Access the user account page to confirm the successful resolution of the lab.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704049208041/c9b45050-024c-40bc-b87c-90bc31c4e832.jpeg align="center")

**Note: Efficient Enumeration** While it's possible to brute-force the login using a single cluster bomb attack, the tutorial emphasizes the efficiency of enumerating a valid username first. This method ensures a more targeted and effective approach to password enumeration.

**Conclusion:** Mastering Burp Intruder is a valuable skill in the realm of web security testing. This tutorial provides a practical walkthrough of password enumeration using Burp Intruder, showcasing how this tool can be harnessed to identify valid usernames and passwords efficiently. As always, conduct security testing responsibly and within the bounds of ethical guidelines.

**Reference**:

[Lab: Username enumeration via different responses | Web Security Academy (portswigger.net)](https://portswigger.net/web-security/authentication/password-based/lab-username-enumeration-via-different-responses)