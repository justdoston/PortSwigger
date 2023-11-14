# File upload vulnerabilities
In this section, you'll learn how simple file upload functions can be used as a powerful vector for a number of high-severity attacks. We'll show you how to bypass common defense mechanisms in order to upload a web shell, enabling you to take full control of a vulnerable web server. Given how common file upload functions are, knowing how to test them properly is essential knowledge.
![image](https://github.com/offensivecyber03/PortSwigger/assets/71892943/8b7fe1cc-9e41-4cd7-ba60-beea6984ea36)

From a security perspective, the worst possible scenario is when a website allows you to upload server-side scripts, such as PHP, Java, or Python files, and is also configured to execute them as code. This makes it trivial to create your own web shell on the server.

`
Web shell
A web shell is a malicious script that enables an attacker to execute arbitrary commands on a remote web server
simply by sending HTTP requests to the right endpoint.
`

If you're able to successfully upload a web shell, you effectively have full control over the server. This means you can read and write arbitrary files, exfiltrate sensitive data, even use the server to pivot attacks against both internal infrastructure and other servers outside the network. For example, the following PHP one-liner could be used to read arbitrary files from the server's filesystem:

```bash
<?php echo file_get_contents('/path/to/target/file'); ?>
```
Once uploaded, sending a request for this malicious file will return the target file's contents in the response.


# Basic Lab

1) Shell php file `<?php echo file_get_contents('/home/carlos/secret'); ?>`
2) After uploading browse to that file according to name
3) Then content of secret file will be revealed.
