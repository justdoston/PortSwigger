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
