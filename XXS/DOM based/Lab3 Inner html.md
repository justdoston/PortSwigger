# DOM XSS in innerHTML sink using source location.search

The `innerHTML` sink doesn't accept script elements on any modern browser, nor will `svg onload` events fire.
This means you will need to use alternative elements like `img` or `iframe`. Event handlers such as onload and onerror can be used in conjunction with these elements. For example:
```bash
element.innerHTML='... <img src=1 onerror=alert(document.domain)> ...'
```
 # Lab
This lab contains a DOM-based cross-site scripting vulnerability in the search blog functionality. It uses an `innerHTML` assignment, which changes the HTML contents of a div element, using data from `location.search`.

Enter the following to search box:
```bash
<img src=1 onerror=alert(1)>
```
We can determine sink using `DOM invader` tool from burp suite
