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
