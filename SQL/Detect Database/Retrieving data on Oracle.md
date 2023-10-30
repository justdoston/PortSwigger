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
