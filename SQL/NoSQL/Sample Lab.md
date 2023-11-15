# Summary
Detect NoSQL injection vulnerability and retrieve other data.

1) In Repeater, submit a `'` character in the category parameter. Notice that this causes a JavaScript syntax error. This may indicate that the user input was not filtered or sanitized correctly.
2) Submit a valid JavaScript payload in the value of the category query parameter. You could use the following payload:<br>`Gifts'+'`<br>We have to URL encode with Ctrl+U
