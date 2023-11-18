# What is blind XXE?

Blind XXE vulnerabilities arise where the application is vulnerable to [XXE injection](https://portswigger.net/web-security/xxe) but does not return the values of any defined external entities within its responses. 

There are two broad ways in which you can find and exploit blind XXE vulnerabilities:
1) You can trigger out-of-band network interactions, sometimes exfiltrating sensitive data within the interaction data.
2) You can trigger XML parsing errors in such a way that the error messages contain sensitive data.

