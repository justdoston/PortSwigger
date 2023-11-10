# Error based blind

Error-based SQL injection refers to cases where you're able to use error messages to either extract or infer sensitive data
from the database, even in blind contexts.
The possibilities depend on the configuration of the database and the types of errors you're able to trigger:

1) You may be able to induce the application to return a specific error response based on the result of a boolean expression.
You can exploit this in the same way as the [conditional response](https://portswigger.net/web-security/sql-injection/blind#exploiting-blind-sql-injection-by-triggering-conditional-responses) we looked at in the previous section.
see [Exploiting blind SQL injection by triggering conditional errors](https://portswigger.net/web-security/sql-injection/blind#exploiting-blind-sql-injection-by-triggering-conditional-errors)https://portswigger.net/web-security/sql-injection/blind#exploiting-blind-sql-injection-by-triggering-conditional-errors).<br>
2) You may be able to trigger error messages that output the data returned by the query.
This effectively turns otherwise blind SQL injection vulnerabilities into visible ones.
For more information, see [Extracting sensitive data via verbose SQL error messages.](https://portswigger.net/web-security/sql-injection/blind#extracting-sensitive-data-via-verbose-sql-error-messages)
