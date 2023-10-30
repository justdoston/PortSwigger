# Database-specific syntax

On Oracle, every `SELECT` query must use the `FROM` keyword and specify a valid table. 
There is a built-in table on Oracle called `dual` which can be used for this purpose.
```bash
' UNION SELECT NULL FROM DUAL--
```
On MySQL, the double-dash sequence must be followed by a space. 
Alternatively, the hash character `#` can be used to identify a comment.

# Finding columns with a useful data type
 
To know which columns holds string data After you determine the number of required columns 
you can probe each column to test whether it can hold string data.
You can submit a series of `UNION SELECT` payloads that place a string value into each column in turn.
```bash
' UNION SELECT 'a',NULL,NULL,NULL--
' UNION SELECT NULL,'a',NULL,NULL--
' UNION SELECT NULL,NULL,'a',NULL--
' UNION SELECT NULL,NULL,NULL,'a'--
```
If the column data type is not compatible with string data, the injected query will cause a database error, such as:
```bash
Conversion failed when converting the varchar value 'a' to data type int.
```
## Lab
**Task**: Determine number of columns<br>
**Solution**
<br>
First  `order by` function
I send `' order by 1--` until error occurs. Error occured when I send `' order by 4--` which means number of columns are 3
<br>
Second confirm I used  `UNION SELECT` I started to sent `' UNION SELECT NULL` until showing page, when I send
`' UNION SELECT NULL,NULL,NULL--` error gone. This is second confirm database has indeed 3 columns

To determine which columns hold string data I replaced `NULL` whith random data 
For example:
`' UNION SELECT 'a',NULL,NULL--` error will happen when column doesn't hold string data, error will gone when we are right columns


