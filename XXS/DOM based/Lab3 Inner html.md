# DOM XSS in innerHTML sink using source location.search

The `innerHTML` sink doesn't accept script elements on any modern browser, nor will `svg onload` events fire.
This means you will need to use alternative elements like `img` or `iframe`. Event handlers such as onload and onerror can be used in conjunction with these elements. For example:
```bash
element.innerHTML='... <img src=1 onerror=alert(document.domain)> ...'
```
