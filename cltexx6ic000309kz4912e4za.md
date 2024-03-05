---
title: "Lab: SQL injection UNION attack, finding a column containing text"
datePublished: Tue Mar 05 2024 22:27:15 GMT+0000 (Coordinated Universal Time)
cuid: cltexx6ic000309kz4912e4za
slug: lab-sql-injection-union-attack-finding-a-column-containing-text
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1706021860491/a51ee5d6-5fea-4189-9bfb-1c821b4fb2ca.png
tags: cybersecurity-1, websecurity, burpsuite, sqlinjection, sqli, portswigger

---

In this lab, our goal is to determine the number of columns returned by the query, offering a valuable insight into potential SQL injection vulnerabilities.

**Step 1: Intercepting and Modifying Requests with Burp Suite**

Burp Suite, a versatile web application testing tool, provides a powerful platform for identifying and addressing security vulnerabilities. Begin by configuring your browser to route traffic through Burp Proxy, allowing for the interception and modification of HTTP requests. As you interact with the target web application, Burp Suite captures and displays the relevant requests in its proxy.

Identify the request responsible for setting the product category filter and use Burp Suite to intercept and modify this request.

**Step 2: Determining the Number of Columns**

Inject the following payload into the category parameter to discern the number of columns returned by the query:

```plaintext
plaintextCopy code'+UNION+SELECT+NULL,NULL,NULL--
```

Observe the application's response. The use of the **UNION SELECT** statement helps to combine the original query with a null value in each column. If an error occurs, it indicates that the injected payload has interfered with the original SQL query.

**Step 3: Replacing Nulls with Random Values**

To further refine our analysis, try replacing each null value with a random string provided by the lab. For example:

```plaintext
plaintextCopy code'+UNION+SELECT+'abcdef',NULL,NULL--
```

If an error occurs with a particular value, move on to the next null value and try a different string. Iterate through this process until an error disappears, and the application's response indicates a successful injection.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1705772690642/092db485-5469-4dec-b29f-eaa22e9b870a.jpeg align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1705772677566/0e06aa1f-fd1b-457c-b03b-82ef94db89a0.png align="center")

**Conclusion**

Security professionals can use Burp Suite's tools to identify SQL injection vulnerabilities by injecting random strings instead of null values into request parameters. This process helps understand how the application handles different inputs and reveals potential vulnerabilities.

**Reference**:

[https://portswigger.net/web-security/sql-injection](https://portswigger.net/web-security/sql-injection)

[https://portswigger.net/web-security/sql-injection/union-attacks/lab-find-column-containing-text](https://portswigger.net/web-security/sql-injection/union-attacks/lab-find-column-containing-text)