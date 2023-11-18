# How does XSS work?

Cross-site scripting works by manipulating a vulnerable web site so that it returns malicious JavaScript to users. When the malicious code executes inside a victim's browser, the attacker can fully compromise their interaction with the application.
![image](https://github.com/offensivecyber03/PortSwigger/assets/71892943/cf51f5e6-cec0-4918-8c6b-28cdf33f6910)

## What are the types of XSS attacks?
1) [Reflected XSS](https://portswigger.net/web-security/cross-site-scripting#reflected-cross-site-scripting), where the malicious script comes from the current HTTP request.
2) [Stored XSS](https://portswigger.net/web-security/cross-site-scripting#stored-cross-site-scripting), where the malicious script comes from the website's database.
3) [DOM-based XSS](https://portswigger.net/web-security/cross-site-scripting#dom-based-cross-site-scripting), where the vulnerability exists in client-side code rather than server-side code.

## Reflected cross-site scripting
[Reflected XSS](https://portswigger.net/web-security/cross-site-scripting/reflected) is the simplest variety of cross-site scripting. It arises when an application receives data in an HTTP request and includes that data within the immediate response in an unsafe way.

Here is a simple example of a reflected XSS vulnerability:
```bash
https://insecure-website.com/status?message=All+is+well.
<p>Status: All is well.</p>
```
The application doesn't perform any other processing of the data, so an attacker can easily construct an attack like this
```bash
https://insecure-website.com/status?message=<script>/*+Bad+stuff+here...+*/</script>
<p>Status: <script>/* Bad stuff here... */</script></p>
```
## Stored cross-site scripting
[Stored XSS](https://portswigger.net/web-security/cross-site-scripting/stored) (also known as persistent or second-order XSS) arises when an application receives data from an untrusted source and includes that data within its later HTTP responses in an unsafe way.

Here is a simple example of a stored XSS vulnerability. A message board application lets users submit messages, which are displayed to other users:
```bash
<p>Hello, this is my message!</p>
```
The application doesn't perform any other processing of the data, so an attacker can easily send a message that attacks other users:
```bash
<p><script>alert('Hello World Alert!')</script></p>
```

## DOM-based cross-site scripting
[DOM-based XSS](https://portswigger.net/web-security/cross-site-scripting/dom-based) (also known as DOM XSS) arises when an application contains some client-side JavaScript that processes data from an untrusted source in an unsafe way, usually by writing the data back to the DOM.

In the following example, an application uses some JavaScript to read the value from an input field and write that value to an element within the HTML:
```
var search = document.getElementById('search').value;
var results = document.getElementById('results');
results.innerHTML = 'You searched for: ' + search;
```
If the attacker can control the value of the input field, they can easily construct a malicious value that causes their own script to execute:
`You searched for: <img src=1 onerror='/* Bad stuff here... */'>`
