---
title: "Lab: SQL injection UNION attack, determining the number of columns returned by the query"
datePublished: Mon Mar 18 2024 08:48:06 GMT+0000 (Coordinated Universal Time)
cuid: cltwpdtc5000l09l84uuubru1
slug: lab-sql-injection-union-attack-determining-the-number-of-columns-returned-by-the-query
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1706022033844/742ce59d-4bf4-44d2-9999-acc2ed12b612.png
tags: cybersecurity-1, websecurity, burpsuite, sqlinjection, sqli, portswigger, hands-on-labs

---

SQL injection is a serious security risk for web applications, and Burp Suite can be used to identify and address these vulnerabilities. This guide shows how to use Burp Suite to intercept and modify requests, specifically focusing on the product category filter. By leveraging Burp Suite's tools, we can uncover potential SQL injection weaknesses and protect our data.

**Step 1: Intercepting and Modifying the Request with Burp Suite**

Burp Suite, a robust web application testing tool, empowers security professionals to identify and mitigate potential threats. Begin by configuring your browser to route traffic through Burp Proxy, allowing for the interception and modification of HTTP requests. As you interact with the target web application, Burp Suite captures and displays the relevant requests.

Identify the request responsible for setting the product category filter and use Burp Suite to intercept and modify this request.

**Step 2: Triggering an Error with '+UNION+SELECT+NULL--**

Inject the following payload into the category parameter to introduce a deliberate error:

```plaintext
plaintextCopy code'+UNION+SELECT+NULL--
```

Observe the application's response. The intentional error is introduced to determine if the application is vulnerable to SQL injection. If an error occurs, it indicates that the injected payload has interfered with the original SQL query.

**Step 3: Incrementally Adding Null Values**

Now, modify the category parameter to add an additional column containing a null value:

```plaintext
plaintextCopy code'+UNION+SELECT+NULL,NULL--
```

Continue adding null values incrementally until the error disappears, and the response includes additional content containing the null values. This step is crucial for identifying the number of columns in the original query and understanding how the application handles the injected null values.

Inspect the application's responses carefully, paying attention to changes in the content length and structure. As you add more null values, you may notice the error disappearing, indicating a successful injection.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1705769462442/6bee616f-bd04-4e0d-bb43-cebad02e4ebd.png align="center")

**Conclusion**

Using Burp Suite, security professionals can identify SQL injection vulnerabilities in web applications by manipulating requests and observing the server's responses. By injecting null values into the request parameters, the query's structure can be analyzed, revealing potential weaknesses.al weaknesses.

**Reference**:

[https://portswigger.net/web-security/sql-injection](https://portswigger.net/web-security/sql-injection)

[https://portswigger.net/web-security/sql-injection/union-attacks/lab-determine-number-of-columns](https://portswigger.net/web-security/sql-injection/union-attacks/lab-determine-number-of-columns)