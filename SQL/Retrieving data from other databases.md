# Retrieving data from other database tables

You can use the `UNION` keyword to execute an additional `SELECT` query and append the results to the original query.

For example, if an application executes the following query containing the user input `Gifts`:
```bash
SELECT name, description FROM products WHERE category = 'Gifts'
```
An attacker can submit the input:
```bash
' UNION SELECT username, password FROM users--
```

