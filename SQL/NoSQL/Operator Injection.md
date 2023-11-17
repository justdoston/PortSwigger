# Detecting operator injection in MongoDB
Consider a vulnerable application that accepts a username and password in the body of a `POST` request:
```bash
{"username":"wiener","password":"peter"}
```
Test each input with a range of operators. For example, to test whether the username input processes the query operator, you could try the following injection:
```bash
{"username":{"$ne":"invalid"},"password":{"peter"}}
```
If the `$ne` operator is applied, this queries all users where the username is not equal to invalid.

If both the username and password inputs process the operator, it may be possible to bypass authentication using the following payload:
```bash
{"username":{"$ne":"invalid"},"password":{"$ne":"invalid"}}
```
This query returns all login credentials where both the username and password are not equal to invalid. As a result, you're logged into the application as the first user in the collection.
