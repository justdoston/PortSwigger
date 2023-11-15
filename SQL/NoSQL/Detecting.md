# Detecting syntax injection in MongoDB

Consider a shopping application that displays products in different categories. When the user selects the **Fizzy drinks** category, their browser requests the following URL:
```bash
https://insecure-website.com/product/lookup?category=fizzy
```
