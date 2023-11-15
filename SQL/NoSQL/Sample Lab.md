# Summary
Detect NoSQL injection vulnerability and retrieve other data.

1) In Repeater, submit a `'` character in the category parameter. Notice that this causes a JavaScript syntax error. This may indicate that the user input was not filtered or sanitized correctly.
2) Submit a valid JavaScript payload in the value of the category query parameter. You could use the following payload:<br>`Gifts'+'`<br>We have to URL encode with Ctrl+U<br> Notice that it doesn't cause a syntax error. This indicates that a form of server-side injection may be occurring.
3) Identify whether you can inject boolean conditions to change the response:<br>Insert a false condition in the category parameter. For example:<br>`Gifts' && 0 && 'x` !URL ENCODE!<br>Insert a true condition in the category parameter. For example:<br>`Gifts' && 1 && 'x` Notice that products in the **Gifts** category are retrieved.
