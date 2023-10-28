# SSRF attacks against the serve

In an SSRF attack against the server, the attacker causes the application to make an HTTP request back to the server 
that is hosting the application, via its loopback network interface. This typically involves supplying a URL with a hostname 
like `127.0.0.1` (a reserved IP address that points to the loopback adapter) or `localhost` 
(a commonly used name for the same adapter).


For example, imagine a shopping application that lets the user view whether an item is in stock in a particular store. 
To provide the stock information, the application must query various back-end REST APIs.
It does this by passing the URL to the relevant back-end API endpoint via a front-end HTTP request. 
When a user views the stock status for an item, their browser makes the following request:
```bash
POST /product/stock HTTP/1.0
Content-Type: application/x-www-form-urlencoded
Content-Length: 118

stockApi=http://stock.weliketoshop.net:8080/product/stock/check%3FproductId%3D6%26storeId%3D1
```
This causes the server to make a request to the specified URL, retrieve the stock status, and return this to the user.
<br>
In this example, an attacker can modify the request to specify a URL local to the server:
```bash
POST /product/stock HTTP/1.0
Content-Type: application/x-www-form-urlencoded
Content-Length: 118

stockApi=http://localhost/admin
```
<br>

The server fetches the contents of the /admin URL and returns it to the user.

An attacker can visit the `/admin` URL, but the administrative functionality is normally only accessible to authenticated users.
This means an attacker won't see anything of interest. However, if the request to the `/admin` 
URL comes from the local machine, the normal access controls are bypassed. 
The application grants full access to the administrative functionality, because the request appears to originate 
from a trusted location.
