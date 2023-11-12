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
