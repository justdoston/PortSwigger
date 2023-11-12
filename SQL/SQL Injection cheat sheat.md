## String concatenation
You can concatenate together multiple strings to make a single string.

**Oracle:** `'foo'||'bar'`<br>
**Microsoft:** `'foo'+'bar'`<br>
**PostgreSQL:**  `'foo'||'bar'`<br>
**Mysql:** `'foo' 'bar'` and `CONCAT('foo','bar')` <br>

## Substring
You can extract part of a string, from a specified offset with a specified length. Note that the offset index is 1-based. 
Each of the following expressions will return the string ba.

**Oracle**	`SUBSTR('foobar', 4, 2)`<br>
**Microsoft** `SUBSTRING('foobar', 4, 2)`<br>
**PostgreSQL**	`SUBSTRING('foobar', 4, 2)`<br>
**MySQL**	`SUBSTRING('foobar', 4, 2)`<br>

## Database version
You can query the database to determine its type and version. This information is useful when formulating more complicated attacks.

**Oracle**	`SELECT banner FROM v$version` and `SELECT version FROM v$instance`<br>
**Microsoft**	`SELECT @@version`<br>
**PostgreSQL**	`SELECT version()`<br>
**MySQL**	`SELECT @@version`<br>

## Database contents

**Oracle:**	`SELECT * FROM all_tables`<br>`SELECT * FROM all_tab_columns WHERE table_name = 'TABLE-NAME-HERE'`<br>
**Microsoft:** `SELECT * FROM information_schema.tables`<br>
`SELECT * FROM information_schema.columns WHERE table_name = 'TABLENAME'`<br>
