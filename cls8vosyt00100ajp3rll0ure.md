---
title: "Lab: SQL injection attack, querying the database type and version on MySQL and Microsoft"
datePublished: Mon Feb 05 2024 11:58:26 GMT+0000 (Coordinated Universal Time)
cuid: cls8vosyt00100ajp3rll0ure
slug: lab-sql-injection-attack-querying-the-database-type-and-version-on-mysql-and-microsoft
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1706022278337/32c6bd58-49ce-4967-894f-e3423aa0e1c5.png
tags: cybersecurity-1, websecurity, burpsuite, sqlinjection, sqli, portswigger, handson

---

We will explore the practical application of Burp Suite to identify and exploit SQL injection vulnerabilities, shedding light on potential risks and the importance of secure coding practices.

**Step 1: Understanding the Basics**

SQL injection occurs when an attacker manipulates input data to inject malicious SQL queries into an application's database. Burp Suite, a widely-used cybersecurity tool, provides a comprehensive set of features for analyzing web application security. Our goal is to use Burp Suite to intercept and modify requests, allowing us to identify and address SQL injection vulnerabilities.

**Step 2: Intercepting and Modifying Requests**

Start by configuring your browser to route traffic through Burp Proxy. This enables the interception of HTTP requests, giving you the ability to analyze and modify them before reaching the server. Navigate to the web application, and as you interact with it, Burp Suite will capture the requests in the proxy.

Identify the request responsible for setting the product category filter. Once identified, use Burp Suite to intercept and modify this specific request.

**Step 3: Determining the Number of Columns**

To exploit SQL injection, it's crucial to understand the structure of the database query. In the payload for the category parameter, inject the following SQL statement:

```plaintext
plaintextCopy code'+UNION+SELECT+'abc','def'#
```

This payload employs the **UNION SELECT** statement to append an additional query to the original one. The goal is to determine the number of columns returned by the query and identify which columns contain text data. If successful, the application's response will display two columns (**'abc' and 'def'**).

**Step 4: Verifying the Result**

Inspect the application's response to verify that the query is indeed returning two columns, both of which contain text. This step confirms the existence of a potential SQL injection vulnerability in the product category filter.

**Step 5: Displaying Database Version**

Now that we have identified potential vulnerabilities, let's proceed to extract information about the database version. Inject the following payload into the category parameter:

```plaintext
plaintextCopy code'+UNION+SELECT+@@version,+NULL#
```

This payload retrieves the database version using the **@@version** function. If successful, the application's response will provide insights into the underlying database technology.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1705750298424/d938ac39-58a5-47f0-9171-236c7c9ec283.png align="left")

**Conclusion:**

By actively engaging with Burp Suite and understanding the nuances of SQL injection, security professionals and developers can bolster the security of web applications. It's essential to conduct regular security assessments, implement secure coding practices, and stay informed about emerging threats to create robust and resilient digital experiences for users.

**Reference**:

[https://portswigger.net/web-security/sql-injection](https://portswigger.net/web-security/sql-injection)

[https://portswigger.net/web-security/sql-injection/examining-the-database/lab-querying-database-version-mysql-microsoft](https://portswigger.net/web-security/sql-injection/examining-the-database/lab-querying-database-version-mysql-microsoft)