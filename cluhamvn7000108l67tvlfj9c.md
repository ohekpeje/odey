---
title: "Lab: SQL injection UNION attack, retrieving data from other tables"
datePublished: Mon Apr 01 2024 18:38:24 GMT+0000 (Coordinated Universal Time)
cuid: cluhamvn7000108l67tvlfj9c
slug: lab-sql-injection-union-attack-retrieving-data-from-other-tables
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1706022983477/8e16fbdf-57a2-4e77-8f34-6828edbf7fed.png
tags: cybersecurity-1, websecurity, burpsuite, sqlinjection, sqli, portswigger, hands-on-labs

---

In this educational guide, we will walk through the process of using Burp Suite to intercept and modify requests, focusing on the product category filter. Our objective is to unveil potential SQL injection vulnerabilities, understand the database structure, and retrieve sensitive information.

**Step 1: Intercepting and Modifying Requests with Burp Suite**

Burp Suite, a powerful tool in the cybersecurity arsenal, allows for the interception and modification of HTTP requests. Begin by configuring your browser to route traffic through Burp Proxy, facilitating the interception of requests. As you interact with the target web application, Burp Suite captures and displays the relevant requests.

Identify the request responsible for setting the product category filter and use Burp Suite to intercept and modify this specific request.

**Step 2: Determining the Number of Columns and Text Data**

Inject the following payload into the category parameter to understand the structure of the database query:

```plaintext
plaintextCopy code'+UNION+SELECT+'abc','def'--
```

Observe the application's response. The use of the UNION SELECT statement combines the original query with two text values ('abc' and 'def'). Verify that the query is returning two columns, both containing text data. This confirmation is crucial for identifying potential SQL injection vulnerabilities.

**Step 3: Retrieving Usernames and Passwords**

Now that we have identified a potential vulnerability, proceed to retrieve the contents of the users table using the following payload:

```plaintext
plaintextCopy code'+UNION+SELECT+username,+password+FROM+users--
```

Inspect the application's response to verify that it contains usernames and corresponding hashed passwords. This step confirms the extent of the vulnerability and highlights the importance of addressing it promptly.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1705774405531/ed3c310f-f89b-4018-bcd1-9b8484d3d022.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1705774439262/2e4fc584-c7b0-4561-86c8-6eb19fb77f8a.png align="center")

**Conclusion**

Harnessing Burp Suite's capabilities, security professionals can effectively identify SQL injection vulnerabilities by actively intercepting, modifying, and analyzing web application requests. This process provides crucial insights into potential security risks and helps protect sensitive data.

**Reference**:

[https://portswigger.net/web-security/sql-injection](https://portswigger.net/web-security/sql-injection)

[https://portswigger.net/web-security/sql-injection/union-attacks](https://portswigger.net/web-security/sql-injection/union-attacks)

[https://portswigger.net/web-security/sql-injection/union-attacks/lab-retrieve-data-from-other-tables](https://portswigger.net/web-security/sql-injection/union-attacks/lab-retrieve-data-from-other-tables)