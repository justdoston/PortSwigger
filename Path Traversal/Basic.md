# Path traversal
![image](https://github.com/offensivecyber03/PortSwigger/assets/71892943/220a2957-4a74-4b6b-b6d3-91db208559cf)

## What is path traversal?

Path traversal is also known as directory traversal. 
These vulnerabilities enable an attacker to read arbitrary files on the server that is running an application. This might include:
<br>
Application code and data.<br>
Credentials for back-end systems.<br>
Sensitive operating system files.<br>

## Reading arbitrary files via path traversal

Imagine a shopping application that displays images of items for sale. This might load an image using the following HTML:<br>
```bash
<img src="/loadImage?filename=218.png">
```
The `loadImage` URL takes a filename parameter and returns the contents of the specified file.
<br>
The image files are stored on disk in the location /var/www/images/.
To return an image, the application appends the requested filename to this base directory and uses a filesystem API to read the contents of the file.
In other words, the application reads from the following file path:
```bash
/var/www/images/218.png
```
This application implements no defenses against path traversal attacks. 
As a result, an attacker can request the following URL to retrieve the `/etc/passwd` file from the server's filesystem:
```bash
https://insecure-website.com/loadImage?filename=../../../etc/passwd
```
This causes the application to read from the following file path:
```bash
/var/www/images/../../../etc/passwd
```
In unix based operating system `../` is valid directory traversal sequences. In windows based operating system<br>
both `../` and `..\` are valid directory traversal sequences.
Here is example directory traversal for windows based system:
```bash
https://insecure-website.com/loadImage?filename=..\..\..\windows\win.ini
```






