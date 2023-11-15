# Detecting syntax injection in MongoDB

Consider a shopping application that displays products in different categories. When the user selects the **Fizzy drinks** category, their browser requests the following URL:
```bash
https://insecure-website.com/product/lookup?category=fizzy
```
This causes the application to send a JSON query to retrieve relevant products from the `product` collection in the MongoDB database:
```bash
this.category == 'fizzy'
```

To test whether the input may be vulnerable, submit a fuzz string in the value of the `category` parameter. An example string for MongoDB is:
```
'"`{
;$Foo}
$Foo \xYZ
```
Use this fuzz string to construct the following attack:
```bash
https://insecure-website.com/product/lookup?category='%22%60%7b%0d%0a%3b%24Foo%7d%0d%0a%24Foo%20%5cxYZ%00
```
If this causes a change from the original response, this may indicate that user input isn't filtered or sanitized correctly.

**Note:**
_NoSQL injection vulnerabilities can occur in a variety of contexts, and you need to adapt your fuzz strings accordingly. Otherwise, you may simply trigger validation errors that mean the application never executes your query.In this example, we're injecting the fuzz string via the URL, so the string is URL-encoded. In some applications, you may need to inject your payload via a JSON property instead. In this case, this payload would become_ 

'\"`{\r;$Foo}\n$Foo \\xYZ\u0000

## Confirming conditional behavior

After detecting a vulnerability, the next step is to determine whether you can influence boolean conditions using NoSQL syntax.

To test this, send two requests, one with a false condition and one with a true condition. For example you could use the conditional statements `' && 0 && 'x` and `' && 1 && 'x` as follows:
```bash
https://insecure-website.com/product/lookup?category=fizzy'+%26%26+0+%26%26+'x
```
and
```bash
https://insecure-website.com/product/lookup?category=fizzy'+%26%26+1+%26%26+'x
```
If the application behaves differently, this suggests that the false condition impacts the query logic, but the true condition doesn't. This indicates that injecting this style of syntax impacts a server-side query.

## Overriding existing conditions

Now that you have identified that you can influence boolean conditions, you can attempt to override existing conditions to exploit the vulnerability. For example, you can inject a JavaScript condition that always evaluates to true, such as `'||1||'`:
```bash
https://insecure-website.com/product/lookup?category=fizzy%27%7c%7c%31%7c%7c%27
```
This results in the following MongoDB query:
```bash
this.category == 'fizzy'||'1'=='1'
```
As the injected condition is always true, the modified query returns all items. This enables you to view all the products in any category, including hidden or unknown categories.
