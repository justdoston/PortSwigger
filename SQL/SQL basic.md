# How to detect SQL injection vulnerabilities
You can detect SQL injection manually using a systematic set of tests against every entry point in the application. To do this, you would typically submit:

1) The single quote character `'` and look for errors or other anomalies.
<br>
2) Some SQL-specific syntax that evaluates to the base (original) value of the entry point, and to a different value, and look for systematic
differences in the application responses.
<br>
3) Boolean conditions such as `OR 1=1` and `OR 1=2`, and look for differences in the application's responses.
<br>
4) Payloads designed to trigger time delays when executed within a SQL query, and look for differences in the time taken to respond.
5) OAST payloads designed to trigger an out-of-band network interaction when executed within a SQL query, and monitor any resulting interactions

# SQL injection in different parts of the query

Most SQL injection vulnerabilities occur within the `WHERE` clause of a `SELECT` query. Most experienced testers are familiar with this type of SQL injection.<br>
Some other common locations where SQL injection arises are:
In `UPDATE` statements, within the updated values or the `WHERE` clause.<br>
In `INSERT` statements, within the inserted values.<br>
In `SELECT` statements, within the table or column name<br>
In `SELECT` statements, within the ORDER BY clause.<br>
