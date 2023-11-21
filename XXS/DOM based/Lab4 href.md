# DOM XSS in jQuery anchor href attribute sink using location.search source

This lab contains a DOM-based cross-site scripting vulnerability in the submit feedback page. It uses the `jQuery` library's $ selector function to find an anchor element, and changes its href attribute using data from `location.search`.

1) On the Submit feedback page, change the query parameter `returnPath` to / followed by a random alphanumeric string.
2) Right-click and inspect the element, and observe that your random string has been placed inside an a href attribute.
3) Change returnPath to:
```bash
javascript:alert(document.cookie)
```
Hit enter and click "back".

## Best explanation on you tube
https://youtu.be/B2E9cEZQQXg
