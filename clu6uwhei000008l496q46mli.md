---
title: "Lab: SQL injection attack, querying the database type and version on Oracle"
datePublished: Mon Mar 25 2024 11:20:17 GMT+0000 (Coordinated Universal Time)
cuid: clu6uwhei000008l496q46mli
slug: lab-sql-injection-attack-querying-the-database-type-and-version-on-oracle
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1706021471242/37104e76-4c54-4a20-b06d-b6127dfad58b.png
tags: oracle, databases, websecurity, burpsuite, sqlinjection, portswigger, hands-on-labs

---

To exploit SQL injection, it's crucial to understand the structure of the database query. Use a payload to determine the number of columns returned by the query and identify columns containing text data. For instance, inject the following payload into the category parameter:

```plaintext
plaintextCopy code'+UNION+SELECT+'abc','def'+FROM+dual--
```

If successful, this payload will append an additional query to the original, resulting in a response that displays two columns ('abc' and 'def') from the 'dual' table. Adjust the payload as needed based on the application's context.

**Displaying Database Version**

Once the number of columns is identified, proceed to extract information about the database, starting with the version. Utilize the following payload in the category parameter:

```plaintext
plaintextCopy code'+UNION+SELECT+BANNER,+NULL+FROM+v$version--
```

This payload leverages the **UNION SELECT** statement to combine the original query with a query that retrieves the version information from the database. The result will be displayed in the application's response, offering insights into the underlying database technology.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1705748363954/c06ed0da-0078-45e1-a3f2-3d80e9804491.png align="left")

**Conclusion**

By utilizing Burp Suite and understanding the mechanics of SQL injection, security professionals can identify and address potential vulnerabilities in web applications. It is essential to conduct ethical hacking responsibly, with the proper authorization, to enhance the security posture of online platforms and protect user data from malicious exploitation. Regular testing and continuous vigilance are key elements in the ongoing battle against cybersecurity threats.

**Reference**:

[https://portswigger.net/web-security/sql-injection](https://portswigger.net/web-security/sql-injection)

[https://portswigger.net/web-security/sql-injection/examining-the-database/lab-querying-database-version-oracle](https://portswigger.net/web-security/sql-injection/examining-the-database/lab-querying-database-version-oracle)