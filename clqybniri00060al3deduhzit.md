---
title: "Lab: Username enumeration via response timing"
datePublished: Wed Jan 03 2024 22:00:09 GMT+0000 (Coordinated Universal Time)
cuid: clqybniri00060al3deduhzit
slug: lab-username-enumeration-via-response-timing
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1703968651753/5063d159-d4f1-45b7-bdb4-bf6b38835692.png
tags: cybersecurity-1, websecurity, burpsuite, lab, portswigger, handson

---

**Introduction:** In the intricate world of web security, identifying vulnerabilities is a skill every cybersecurity enthusiast must hone. This blog post unravels a fascinating lab exercise that delves into the subtleties of username enumeration, showcasing how attackers can exploit nuanced responses to pinpoint valid usernames.

**Lab Overview: Username Enumeration via Subtly Different Responses**

**Step 1: Initiating the Attack** With Burp Suite running, let's kick off the exploration by submitting an invalid username and password. The goal here is to understand how the system responds to such inputs. Highlight the username parameter in the `POST /login` request and send it to Burp Intruder for detailed analysis.

**Step 2: Configuring Payloads in Burp Intruder** Navigate to the Payloads tab within Burp Intruder. Observe that the username parameter is automatically marked as a payload position, indicating it's a key element in our exploration. Ensure that the Simple list payload type is selected and integrate the list of candidate usernames.

**Step 3: Extracting Error Messages** On the Settings tab, under Grep - Extract, click Add. In the ensuing dialog, scroll through the response until you find the familiar error message "Invalid username or password." Use the mouse to highlight the text content of this message. The other settings will automatically adjust. Click OK and initiate the attack.

**Step 4: Analyzing Attack Results** As the attack concludes, pay attention to the results. There will be an additional column containing the extracted error message. By sorting the results using this column, one subtly different entry becomes apparent.

**Step 5: Identifying the Unique Response** Closer inspection reveals a typo in the error message of this particular response - instead of a full stop/period, there is a trailing space. Make a note of the username associated with this distinct response.

**Step 6: Preparing for the Next Attack** Close the initial attack and return to the Positions tab in Burp Intruder. Insert the identified username and add a payload position to the password parameter. The configuration should look like this:

```plaintext
username=identified-user&password=§invalid-password§
```

**Step 7: Executing the Second Attack** On the Payloads tab, clear the list of usernames and replace it with the list of passwords. Initiate the attack.

**Step 8: Recognizing a Successful Response** Upon completion of the second attack, scrutinize the responses. If one of the requests receives a **302 response**, it indicates a successful login attempt. Make a note of this password for the final stage.

**Step 9: Logging in to Solve the Lab** Utilize the identified username and password to log in successfully. Access the user account page to effectively solve the lab.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704049338887/7cd19cf8-833a-4258-95be-33fd80a7e729.jpeg align="center")

**Note: The Efficiency of Enumeration** While it's plausible to brute-force login credentials using a single cluster bomb attack, this lab underscores the efficiency of enumerating a valid username first. This targeted approach not only saves time but also optimizes resources compared to blind brute-force attempts.

**Conclusion:** This lab exercise provides a hands-on exploration of username enumeration, demonstrating how subtle differences in responses can be exploited by attackers. By delving into these nuances, cybersecurity enthusiasts and professionals can enhance their ability to detect and address vulnerabilities in web applications. Always approach such exercises responsibly, prioritizing ethical and secure practices to contribute to a safer digital environment.

**Reference:**

[Lab: Username enumeration via response timing | Web Security Academy (portswigger.net)](https://portswigger.net/web-security/authentication/password-based/lab-username-enumeration-via-response-timing)