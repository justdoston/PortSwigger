# Exploiting blind OS command injection by redirecting output

You can redirect the output from the injected command into a file within the web root that you can then retrieve using the browser. For example, if the application serves static resources from the filesystem location `/var/www/static`, then you can submit the following input:
```bash
& whoami > /var/www/static/whoami.txt &
```
The `>` character sends the output from the `whoami` command to the specified file. You can then use the browser to fetch `https://vulnerable-website.com/whoami.txt` to retrieve the file, and view the output from the injected command.

# Example Lab

1) Use Burp Suite to intercept and modify the request that submits feedback.
2) Modify the email parameter, changing it to:<br> `email=||whoami>/var/www/images/output.txt||`
3) Now use Burp Suite to intercept and modify the request that loads an image of a product.
4) Modify the `filename` parameter, changing the value to the name of the file you specified for the output of the injected command:<br>`filename=output.txt`
5) Observe that the response contains the output from the injected command.

## Explanation from you tube:
https://youtu.be/4Wl9Ap8cmqQ
