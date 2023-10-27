# Broken access control resulting from platform misconfiguration

Some applications enforce access controls at the platform layer. they do this by restricting 
access to specific URLs and HTTP methods based on the user's role. 
For example, an application might configure a rule as follows:
```bash
DENY: POST, /admin/deleteUser, managers
```
This rule denies access to the POST method on the URL /admin/deleteUser, for users in the managers group. 
Various things can go wrong in this situation, leading to access control bypasses.

Some application frameworks support various non-standard HTTP headers that can be used to override the URL in the original request, 
such as `X-Original-URL` and `X-Rewrite-URL`. If a website uses rigorous front-end controls to restrict access based on the URL, 
but the application allows the URL to be overridden via a request header, 
then it might be possible to bypass the access controls using a request like the following:
```bash
POST / HTTP/1.1
X-Original-URL: /admin/deleteUser
```
# Lab
![image](https://github.com/offensivecyber03/PortSwigger/assets/71892943/af479c26-91e7-46c8-b2c4-2abf50764cec)<br>

Try to load /admin and observe that you get blocked. Notice that the response is very plain, suggesting it may originate from a front-end system.
Send the request to Burp Repeater. 
<br>Change the URL in the request line to / and add the HTTP header X-Original-URL: /invalid. Observe that the application returns a "not found" response. This indicates that the back-end system is processing the URL from the X-Original-URL header.
<br>Change the value of the X-Original-URL header to /admin. Observe that you can now access the admin page.
<br>To delete carlos, add ?username=carlos to the real query string, and change the X-Original-URL path to /admin/delete.
