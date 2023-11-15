# Insufficient blacklisting of dangerous file types

The practice of blacklisting is inherently flawed as it's difficult to explicitly block every possible file extension that could be used to execute code. Such blacklists can sometimes be bypassed by using lesser known, alternative file extensions that may still be executable, such as .php5, .shtml, and so on.

## Overriding the server configuration

As we discussed in the previous section, servers typically won't execute files unless they have been configured to do so. For example, before an Apache server will execute PHP files requested by a client, developers might have to add the following directives to their `/etc/apache2/apache2.conf` file:
```
LoadModule php_module /usr/lib/apache2/modules/libphp.so
AddType application/x-httpd-php .php
```

Similarly, developers can make directory-specific configuration on IIS servers using a web.config file. This might include directives such as the following, which in this case allows JSON files to be served to users:
```
<staticContent>
    <mimeMap fileExtension=".json" mimeType="application/json" />
</staticContent>
```

Web servers use these kinds of configuration files when present, but you're not normally allowed to access them using HTTP requests. However, you may occasionally find servers that fail to stop you from uploading your own malicious configuration file. In this case, even if the file extension you need is blacklisted, you may be able to trick the server into mapping an arbitrary, custom file extension to an executable MIME type.


# Lab

1) I tried to send malicious php payload and got the response that I am not allowed to upload .php file.
2) In Burp's proxy history, find the `POST /my-account/avatar` request that was used to submit the file upload. In the response, notice that the headers reveal that you're talking to an Apache server. Send this request to Burp Repeater.
3) In request I have to change following headers:<br>Change the value of the `filename` parameter to `.htaccess`.<br>Change the value of the `Content-Type` header to `text/plain`<br>Replace the contents of the file (your PHP payload) with the following Apache directive:<br>`AddType application/x-httpd-php .l33t`<br>
![image](https://github.com/offensivecyber03/PortSwigger/assets/71892943/1c861057-e665-4546-83c7-8ea0e3ae7007)
![image](https://github.com/offensivecyber03/PortSwigger/assets/71892943/e8c0efbb-61b6-4674-b715-0dbdf3abf014)<br>
4) Now come back to original reqesut using back arrow or change this headers:<br>`filename` parametr to `exploit.l33t`<br>`Content-Type` header to `application/php`

