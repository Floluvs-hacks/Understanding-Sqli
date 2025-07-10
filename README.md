# Understanding-Sqli
# What is SQL Injection?  
**Understanding One of the Most Dangerous Web Vulnerabilities Through Practical Examples**

## Introduction? Of Course
SQL Injection (SQLi) is one of the most well-known and dangerous web application vulnerabilities. It allows attackers to interfere with the queries that an application makes to its database,potentially leading to **unauthorized data access**, **data loss**, or even **full system compromise**.

In this post, I break down the concept of SQL Injection in a beginner-friendly way, and share some hands-on examples I practiced during my learning.

##  What is SQL Injection?
SQL Injection occurs when an application takes **user input** and incorporates it **directly into an SQL query** without proper validation or sanitization.If not handled correctly, this input can be manipulated to alter the logic of the original query.

For example:
sql
SELECT * FROM users WHERE username = 'admin' AND password = '1234';

If this query above is built like:

```python
query = "SELECT * FROM users WHERE username = '" + user_input + "';"
```
And the user enters:
```sql
' OR '1'='1
```

The query becomes:

```sql
SELECT * FROM users WHERE username = '' OR '1'='1';
```

Now the condition always evaluates to granting unauthorized access.

##  A Simple Practical Example
I used a vulnerable test website like [testphp.vulnweb.com](http://testphp.vulnweb.com) to try the following:
1. Login Bypass
**Original form fields:**
```html
Username: admin
Password: admin123
```

**Injected input:**
```plaintext
Username: ' OR '1'='1
Password: anything
```

**Effect:** Logged in without needing valid credentials.

## Types of SQL Injection
During practice, I learned that SQLi comes in different forms:

1. **In-band SQLi** – Error-based and Union-based injections  
2. **Blind SQLi** – True/false-based or time-based (no error messages)  
3. **Out-of-band SQLi** – Uses external channels like DNS or HTTP to extract data  

Each type presents different challenges depending on how the web app handles errors and displays responses.

---

## Prevention Techniques
Understanding SQLi also taught me about secure coding practices. Here are a few prevention strategies I explored:

**Use Prepared Statements (Parameterized Queries)**  
  Example in Python with SQLite:
  ```python
  cursor.execute("SELECT * FROM users WHERE username = ?", (user_input,))
  ```
- **Input Validation & Escaping**
- **Use ORM frameworks**
- **Least Privilege Access** – Don’t let apps connect with full DB admin rights
- **Web Application Firewalls (WAF)** – To catch basic attack patterns


##  My Final Thoughts?
Learning about SQL Injection gave me a real-world understanding of how insecure code can be exploited and how developers and security professionals must think critically about **how data is handled**. It’s one of those classic vulnerabilities that every cybersecurity learner must experience firsthand,responsibly and ethically. Also never trust user input, REMEMBER TO ALWAYS VALIDATE AND SANITIZE 
                  PREVENTION IS BETTER THAN PATCHING A BREACHED DATABASE


