# Using a SQL injection UNION attack to retrieve interesting data

Suppose that:
1) The original query returns two columns, both of which can hold string data.
2) The injection point is a quoted string within the `WHERE` clause.
3) The database contains a table called `users` with the columns `username` and `password`

In this example, you can retrieve the contents of the users table by submitting the input:
```bash
' UNION SELECT username, password FROM users--
```
In order to perform this attack, you need to know 
that there is a table called `users` with two columns called `username` and `password`.

