# Subverting application logic

Imagine an application that lets users log in with a `username` and `password`. 
If a user submits the username wiener and the password bluecheese, the application checks the credentials by performing the following SQL query:
```bash
SELECT * FROM users WHERE username = 'wiener' AND password = 'bluecheese'
```
Attacker can bypass login session to adding comment `--` to username which makes comment rest of the query
For example:
```bash
SELECT * FROM users WHERE username = 'administrator'--' AND password = ''
```


https://github.com/offensivecyber03/PortSwigger/assets/71892943/ec627dc2-cf55-4902-82f0-10a2ac0d17bb

