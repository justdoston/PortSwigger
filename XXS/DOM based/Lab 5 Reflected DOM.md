# Reflected DOM XSS

Application uses dangerous `eval()` function.
Here is how application uses it's function:
![image](https://github.com/offensivecyber03/PortSwigger/assets/71892943/152d3688-b08d-4009-a4c9-04c01f54aa5a)

```bash
\"-alert(1)}//
```
Above payload can help us to exploit vulnerability.
As you have injected a backslash and the site isn't escaping them, when the JSON response attempts to escape the opening double-quotes character, it adds a second backslash. The resulting double-backslash causes the escaping to be effectively canceled out. This means that the double-quotes are processed unescaped, which closes the string that should contain the search term.
