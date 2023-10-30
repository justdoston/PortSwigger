# SQL injection UNION attacks

The UNION keyword enables you to execute 
one or more additional SELECT queries and append the results to the original query. For example:
```bash
SELECT a, b FROM table1 UNION SELECT c, d FROM table2
```
This SQL query returns a single result set with two columns, containing values from columns `a` and `b` in `table1` and columns `c` and `d` in `table2`

For a `UNION` query to work, two key requirements must be met:
1) The individual queries must return the same number of columns.
2) The data types in each column must be compatible between the individual queries.

To carry out a SQL injection UNION attack, make sure that your attack meets these two requirements. 
This normally involves finding out:
1) How many columns are being returned from the original query.
2) Which columns returned from the original query are of a suitable data type to hold the results from the injected query.

