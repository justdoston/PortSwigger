# Parameter-based access control methods

Some applications determine the user's access rights or role at login, and then store this information in a user-controllable location. This could be:

A hidden field.<br>
A cookie.<br>
A preset query string parameter.<br>

The application makes access control decisions based on the submitted value. For example:
```bash
https://insecure-website.com/login/home.jsp?admin=true
https://insecure-website.com/login/home.jsp?role=1
```
This approach is insecure because a user can modify the value and access functionality they're not authorized to, such as administrative functions.

# Lab

Browse to /admin and observe that you can't access the admin panel.<br>
Browse to the login page.<br>
In Burp Proxy, turn interception on and enable response interception.<br>
Complete and submit the login page, and forward the resulting request in Burp.<br>
Observe that the response sets the cookie `Admin=false`. Change it to `Admin=true`.<br>
Load the admin panel and delete carlos.
