---
title: "Lab: SQL injection attack, listing the database contents on non-Oracle databases"
datePublished: Mon Apr 08 2024 05:43:06 GMT+0000 (Coordinated Universal Time)
cuid: cluqj0sfn000c08l2azo4a60j
slug: lab-sql-injection-attack-listing-the-database-contents-on-non-oracle-databases
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1706021685701/cd354c6e-fa33-4046-b6c8-d1fd1a2736e7.png
tags: cybersecurity-1, websecurity, burpsuite, sqlinjection, sqli, portswigger, handson

---

In this educational guide, we will explore the practical application of Burp Suite to identify and exploit SQL injection vulnerabilities, highlighting the importance of robust security practices.

**Step 1: Intercepting and Modifying Requests with Burp Suite**

Burp Suite serves as a powerful ally in identifying and mitigating security risks. Start by configuring your browser to route traffic through Burp Proxy, enabling the interception of HTTP requests. Navigate to the target web application, and as you interact with it, Burp Suite will capture the relevant requests in the proxy.

Identify the request responsible for setting the product category filter, and use Burp Suite to intercept and modify this specific request.

**Step 2: Determining the Number of Columns**

Inject the following payload into the category parameter to determine the number of columns returned by the query and identify which columns contain text data:

```plaintext
plaintextCopy code'+UNION+SELECT+'abc','def'--
```

Inspect the application's response to verify that the query is returning two columns, both of which contain text. This step confirms the existence of a potential SQL injection vulnerability in the product category filter.

**Step 3: Retrieving the List of Tables in the Database**

Now that we have identified a potential vulnerability, proceed to retrieve the list of tables in the database using the following payload:

```plaintext
plaintextCopy code'+UNION+SELECT+table_name,+NULL+FROM+information_schema.tables--
```

Inspect the response to obtain a list of tables in the database. Locate the table that likely contains user credentials.

**Step 4: Retrieving Details of Columns in the User Credentials Table**

Once the user credentials table is identified, use the following payload to retrieve details of the columns in that table (replace 'users\_abcdef' with the actual table name):

```plaintext
plaintextCopy code'+UNION+SELECT+column_name,+NULL+FROM+information_schema.columns+WHERE+table_name='users_abcdef'--
```

Inspect the response to find the names of columns containing usernames and passwords.

**Step 5: Retrieving Usernames and Passwords**

With knowledge of the table and column names, use the following payload to retrieve usernames and passwords for all users (replace **'users\_abcdef', 'username\_abcdef', and 'password\_abcdef**' with the actual table and column names):

```plaintext
plaintextCopy code'+UNION+SELECT+username_abcdef,+password_abcdef+FROM+users_abcdef--
```

Inspect the response to retrieve the usernames and hashed passwords for all users.

**Step 6: Finding the Administrator's Password**

Identify the administrator user and retrieve their hashed password. Utilize secure password-cracking techniques or rainbow tables to obtain the plaintext password.

**Step 7: Logging in as Administrator**

Use the obtained password to log in as the administrator, emphasizing the critical importance of promptly addressing and patching SQL injection vulnerabilities to protect user data and prevent unauthorized access.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1705753518872/2f59828d-4a10-4a82-8a65-da90a6b2aa54.png align="center")

**Conclusion**

By actively engaging with Burp Suite and understanding the mechanics of SQL injection, security professionals and developers can enhance the security posture of web applications. Regular security assessments, coupled with secure coding practices, are essential in safeguarding sensitive information and maintaining the trust of users in an increasingly connected world.

**Reference**:

[https://portswigger.net/web-security/sql-injection](https://portswigger.net/web-security/sql-injection)

[https://portswigger.net/web-security/sql-injection/examining-the-database/lab-listing-database-contents-non-oracle](https://portswigger.net/web-security/sql-injection/examining-the-database/lab-listing-database-contents-non-oracle)