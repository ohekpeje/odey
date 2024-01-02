---
title: "Lab: Username enumeration via subtly different responses"
datePublished: Tue Jan 02 2024 22:00:12 GMT+0000 (Coordinated Universal Time)
cuid: clqww7q5t000108ljey081i6y
slug: lab-username-enumeration-via-subtly-different-responses
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1703967787695/ccad5576-175c-4745-88aa-714b3b68954e.png
tags: cybersecurity-1, websecurity, burpsuite, username, portswigger, handson, hands-on-labs

---

**Introduction:** In the dynamic landscape of web security, the ability to identify vulnerabilities such as username enumeration is crucial. This blog post unravels a lab exercise that focuses on subtleties in responses, showcasing how attackers can exploit subtle differences to enumerate valid usernames.

**Lab Overview: Username Enumeration via Subtly Different Responses**

**Step 1: Initiating the Attack** With Burp Suite running, kick off the process by submitting an invalid username and password. Identify the username parameter in the `POST /login` request and send it to Burp Intruder for further analysis.

**Step 2: Configuring Payloads in Burp Intruder** Navigate to the Payloads tab in Burp Intruder. Observe that the username parameter is automatically designated as a payload position. Ensure the Simple list payload type is selected, and incorporate the list of candidate usernames.

**Step 3: Extracting Error Messages** Move to the Settings tab and, under Grep - Extract, add a grep for the error message "Invalid username or password." Extract this message by highlighting its text content in the response. Click OK and initiate the attack.

**Step 4: Identifying Subtle Differences** After the attack concludes, examine the results, specifically the column containing the extracted error message. Identify a subtly different response, potentially with a typo or variation in the error message. Note this username for further exploitation.

**Step 5: Creating Payload Positions** Close the initial attack and return to the Positions tab. Insert the identified username and add a payload position to the password parameter. The configuration should resemble:

```plaintext
username=identified-user&password=§invalid-password§
```

**Step 6: Executing the Second Attack** On the Payloads tab, clear the list of usernames and replace it with the list of passwords. Initiate the attack.

**Step 7: Recognizing a Successful Response** Upon completion of the attack, observe the responses. If one of the requests receives a 302 response, it indicates a successful login attempt. Make a note of this password for the final stage.

**Step 8: Logging in to Solve the Lab** Log in using the identified username and password. Access the user account page to successfully solve the lab.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704049318647/8c5b3192-9e36-4351-90fa-eae7e3d18f54.jpeg align="center")

**Note: The Efficiency of Enumeration** While it's possible to brute-force login credentials using a single cluster bomb attack, this lab emphasizes the efficiency of enumerating a valid username first. This targeted approach saves time and resources in comparison to blind brute-force attempts.

**Conclusion:** This lab exercise provides hands-on experience in identifying and exploiting subtle responses to enumerate valid usernames. By dissecting the intricacies of web security, enthusiasts and professionals alike can strengthen their ability to secure applications against potential threats. Always approach such exercises responsibly and ethically, prioritizing the enhancement of security measures for a safer digital environment.

**Reference**:

[Lab: Username enumeration via subtly different responses | Web Security Academy (portswigger.net)](https://portswigger.net/web-security/authentication/password-based/lab-username-enumeration-via-subtly-different-responses)