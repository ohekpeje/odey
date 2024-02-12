---
title: "Lab: SQL injection UNION attack, retrieving multiple values in a single column"
datePublished: Mon Feb 12 2024 09:11:52 GMT+0000 (Coordinated Universal Time)
cuid: clsiptkip000209ld6pjmdwho
slug: lab-sql-injection-union-attack-retrieving-multiple-values-in-a-single-column
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1706023808205/0b109589-0ec5-4321-af5b-db3d89d3167c.png
tags: cybersecurity-1, websecurity, burpsuite, sqlinjection, sqli, portswigger, handson

---

In this educational guide, we will delve into the process of leveraging Burp Suite to intercept and modify requests, focusing on the product category filter. Our objective is to uncover potential SQL injection vulnerabilities, understand the database structure, and retrieve sensitive information.

**Step 1: Intercepting and Modifying Requests with Burp Suite**

Burp Suite, a versatile web application testing tool, empowers security professionals to identify and address potential vulnerabilities. Begin by configuring your browser to route traffic through Burp Proxy, allowing for the interception and modification of HTTP requests. As you interact with the target web application, Burp Suite captures and displays the relevant requests.

Identify the request responsible for setting the product category filter and use Burp Suite to intercept and modify this specific request.

**Step 2: Determining the Number of Columns and Text Data**

Inject the following payload into the category parameter to understand the structure of the database query:

```plaintext
plaintextCopy code'+UNION+SELECT+NULL,'abc'--
```

Observe the application's response. The use of the UNION SELECT statement combines the original query with a null value and a text value ('abc'). Verify that the query is returning two columns, with only one containing text data. This insight is crucial for identifying potential SQL injection vulnerabilities.

**Step 3: Retrieving Usernames and Passwords**

Now that a potential vulnerability is identified, proceed to retrieve the contents of the users table using the following payload:

```plaintext
plaintextCopy code'+UNION+SELECT+NULL,username||'~'||password+FROM+users--
```

Inspect the application's response to verify that it contains usernames and corresponding hashed passwords. This step confirms the extent of the vulnerability and emphasizes the importance of addressing it promptly.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1705775969199/b7f46458-12b5-4916-982d-acf96d6adf72.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1705776015724/84dd688e-cf43-4d2c-a529-a75ef63ae4b8.png align="center")

**Conclusion**

SQL injection is a serious threat to web applications, but Burp Suite can help you find and fix these vulnerabilities. By intercepting and modifying requests, Burp Suite lets you identify suspicious behavior and protect your data.

**Reference**:

[https://portswigger.net/web-security/sql-injection](https://portswigger.net/web-security/sql-injection)

[https://portswigger.net/web-security/sql-injection/union-attacks/lab-retrieve-multiple-values-in-single-column](https://portswigger.net/web-security/sql-injection/union-attacks/lab-retrieve-multiple-values-in-single-column)