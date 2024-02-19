---
title: "Lab: SQL injection attack, listing the database contents on Oracle"
datePublished: Mon Feb 19 2024 05:45:40 GMT+0000 (Coordinated Universal Time)
cuid: clssijd0f000m09k146x099wa
slug: lab-sql-injection-attack-listing-the-database-contents-on-oracle
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1706022822851/8c26724c-b42b-4e74-a837-12b465a20f14.png
tags: cybersecurity-1, websecurity, burpsuite, sqlinjection, sqli, portswigger

---

This article aims to provide an educational walkthrough using Burp Suite to identify and exploit SQL injection vulnerabilities, emphasizing the significance of proactive security measures.

**Step 1: Intercepting and Modifying Requests with Burp Suite**

Burp Suite, a powerful web application testing tool, allows us to intercept and modify HTTP requests. Begin by configuring your browser to route traffic through Burp Proxy, enabling the interception of requests. As you interact with the target web application, Burp Suite captures and displays the intercepted requests.

Identify the request responsible for setting the product category filter and use Burp Suite to intercept and modify this specific request.

**Step 2: Determining the Number of Columns**

Inject the following payload into the category parameter to understand the structure of the database query:

```plaintext
plaintextCopy code'+UNION+SELECT+'abc','def'+FROM+dual--
```

Inspect the application's response to verify that the query is returning two columns, both of which contain text. This confirms the potential existence of an SQL injection vulnerability.

**Step 3: Retrieving the List of Tables in the Database**

Proceed to retrieve the list of tables in the database using the following payload:

```plaintext
plaintextCopy code'+UNION+SELECT+table_name,NULL+FROM+all_tables--
```

Inspect the response to obtain a comprehensive list of tables. Identify the table likely to contain user credentials.

**Step 4: Retrieving Details of Columns in the User Credentials Table**

Once the user credentials table is identified, use the following payload to retrieve details of the columns (replace 'USERS\_ABCDEF' with the actual table name):

```plaintext
plaintextCopy code'+UNION+SELECT+column_name,NULL+FROM+all_tab_columns+WHERE+table_name='USERS_ABCDEF'--
```

Examine the response to find the names of columns containing usernames and passwords.

**Step 5: Retrieving Usernames and Passwords**

With knowledge of the table and column names, use the following payload to retrieve usernames and passwords for all users (replace 'USERS\_ABCDEF', 'USERNAME\_ABCDEF', and 'PASSWORD\_ABCDEF' with the actual table and column names):

```plaintext
plaintextCopy code'+UNION+SELECT+USERNAME_ABCDEF,+PASSWORD_ABCDEF+FROM+USERS_ABCDEF--
```

Inspect the response to obtain the usernames and hashed passwords for all users.

**Step 6: Finding the Administrator's Password**

Identify the administrator user and retrieve their hashed password. Employ secure password-cracking techniques to obtain the plaintext password.

**Step 7: Logging in as Administrator**

Utilize the obtained password to log in as the administrator, underscoring the urgency of addressing SQL injection vulnerabilities promptly to safeguard user data and prevent unauthorized access.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1705767605591/c6fab7c8-325a-4a04-ba3f-8f8c2136bb23.png align="center")

**Conclusion**

By actively utilizing tools like Burp Suite and understanding the intricacies of SQL injection, security professionals can bolster the security of web applications. This educational guide serves as a reminder of the importance of proactive testing, continuous vigilance, and adherence to secure coding practices in the ever-evolving landscape of cybersecurity. Regular assessments and swift remediation efforts are critical to maintaining the integrity and trustworthiness of online platforms.

**Reference**:

[https://portswigger.net/web-security/sql-injection](https://portswigger.net/web-security/sql-injection)

[https://portswigger.net/web-security/sql-injection/examining-the-database/lab-listing-database-contents-oracle](https://portswigger.net/web-security/sql-injection/examining-the-database/lab-listing-database-contents-oracle)