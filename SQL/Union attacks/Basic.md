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

# Determining the number of columns required
There are 2 types of method to determine number of columns.

## First method 
one method involves injecting a series of `ORDER BY` clauses and incrementing 
the specified column index until an error occurs.
For example, if the injection point is a quoted string within the `WHERE` clause of the original query, you would submit:
```bash
' ORDER BY 1--
' ORDER BY 2--
' ORDER BY 3--
etc.
```
The column in an `ORDER BY` clause can be specified by its index, so you **don't** need to know the names of any columns.
<br>
When the specified column index **exceeds** the number of actual columns in the result set, the database returns an error, such as:
```bash
The ORDER BY position number 3 is out of range of the number of items in the select list.
```

## Second method
The second method involves submitting a series of UNION SELECT payloads specifying a different number of null values:
```bash
' UNION SELECT NULL--
' UNION SELECT NULL,NULL--
' UNION SELECT NULL,NULL,NULL--
etc.
```
If the number of nulls does not match the number of columns, the database returns an error, such as
```bash
All queries combined using a UNION, INTERSECT or EXCEPT operator must have an equal number of expressions in their target lists.
```

## Lab
**Task:** Determine number of columns
**Solution:** `UNION SELECT NULL,NULL,NULL,NULL--`



