# Injecting operators in MongoDB

Consider a vulnerable application that accepts username and password in the body of a `POST` request:
```bash
{"username":"wiener","password":"peter"}
```
To test whether you can inject operators, you could try adding the $where operator as an additional parameter, then send one request where the condition evaluates to false, and another that evaluates to true. For example:
```bash
{"username":"wiener","password":"peter", "$where":"0"}
{"username":"wiener","password":"peter", "$where":"1"}
```
If there is a difference between the responses, this may indicate that the JavaScript expression in the `$where` clause is being evaluated.

## Extracting field names

If you have injected an operator that enables you to run JavaScript, you may be able to use the keys() method to extract the name of data fields. For example, you could submit the following payload:
```bash
"$where":"Object.keys(this)[0].match('^.{0}a.*')"
```
This inspects the first data field in the user object and returns the first character of the field name. This enables you to extract the field name character by character.

# Lab
![image](https://github.com/offensivecyber03/PortSwigger/assets/71892943/7555fcaf-d511-4715-a638-f20cbf90f82f)
<br>
![image](https://github.com/offensivecyber03/PortSwigger/assets/71892943/d1e3afb1-ba68-484d-afda-405578a5a013)
<br>
![image](https://github.com/offensivecyber03/PortSwigger/assets/71892943/34ade2b8-b092-4d90-acf3-08c7f031b18e)
