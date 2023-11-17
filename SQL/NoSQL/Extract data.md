# Exploiting syntax injection to extract data

In many NoSQL databases, some query operators or functions can run limited JavaScript code, such as MongoDB's `$where` operator and `mapReduce()` function. This means that, if a vulnerable application uses these operators or functions, the database may evaluate the JavaScript as part of the query. You may therefore be able to use JavaScript functions to extract data from the database.

## Exfiltrating data in MongoDB
Consider a vulnerable application that allows users to look up other registered usernames and displays their role. This triggers a request to the URL:
```bash
https://insecure-website.com/user/lookup?username=admin
```
This results in the following NoSQL query of the users collection:
```bash
{"$where":"this.username == 'admin'"}
```
As the query uses the `$where` operator, you can attempt to inject JavaScript functions into this query so that it returns sensitive data. For example, you could send the following payload:
```bash
admin' && this.password[0] == 'a' || 'a'=='b
```
This returns the first character of the user's password string, enabling you to extract the password character by character.

You could also use the JavaScript match() function to extract information. For example, the following payload enables you to identify whether the password contains digits:
```bash
admin' && this.password.match(/\d/) || 'a'=='b
```

# Lab

1) In Burp, go to Proxy > HTTP history. Right-click the `GET /user/lookup?user=wiener` request and select Send to Repeater.
2) Submit a `'` character in the user parameter. Notice that this causes an error. This may indicate that the user input was not filtered or sanitized correctly.
3) Submit a valid JavaScript payload in the user parameter. For example, you could use `wiener'+'` URL ENCODE Notice that it retrieves the account details for the wiener user, which indicates that a form of server-side injection may be occurring.
4) Identify whether you can inject boolean conditions to change the response:<br>Submit:<br>`wiener' && '1'=='2` notice error appeared<br>Submit:<br>`wiener' && '1'=='1`notice error is gone 
