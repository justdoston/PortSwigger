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

1) Visit web site, load and capture request using burp suite send it to repeater
2) Modify the TrackingId cookie, appending a single quotation mark to it:
```bash
TrackingId=xyz'
```
Verify error happened<br>
3) Now change it to two quotation marks:
```bash
TrackingId=xyz''
```
Verify that the error disappears. This suggests that a syntax error (in this case, the unclosed quotation mark) is having a detectable effect on the response.<br>
4) You now need to confirm that the server is interpreting the injection as a SQL query i.e. that the error is a SQL syntax error as opposed to any other kind of error. To do this, you first need to construct a subquery using valid SQL syntax. Try submitting:
