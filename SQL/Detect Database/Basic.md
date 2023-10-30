# Querying the database type and version

The following are some queries to determine the database version for some popular database types:

Database type	                           Query
Microsoft, MySQL                         `SELECT @@version`
Oracle                                   `SELECT * FROM v$version`
Postgresql                               `SELECT version()`

