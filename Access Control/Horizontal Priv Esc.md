# Horizontal privilege escalation

If user able to access to another users account, page it will be horizontal privilege escalation<br>
Horizontal privilege escalation attacks may use similar types of exploit methods to vertical privilege escalation.
For example, a user might access their own account page using the following URL:
```bash
https://insecure-website.com/myaccount?id=123
```
# Lab
Find a blog post by `carlos`.<br>
Click on carlos and observe that the URL contains his user ID. Make a note of this `ID`.<br>
Log in using the supplied credentials and access your account page.<br>
Change the "id" parameter to the saved user `ID`.<br>
Retrieve and submit the API key.
