# Unprotected functionality

At its most basic, vertical privilege escalation arises where an application does not enforce any protection for sensitive functionality.
For example, administrative functions might be linked from an administrator's welcome page but not from a user's welcome page.

For example, a website might host sensitive functionality at the following URL:
```bash
https://insecure-website.com/admin
```
Even if the URL isn't disclosed anywhere, an attacker may be able to use a wordlist to brute-force the location of the sensitive functionality.


In some cases, sensitive functionality is concealed by giving it a less predictable URL. This is an example of so-called "security by obscurity". 

However, hiding sensitive functionality does not provide effective access control because users might discover the obfuscated URL in a number of ways.
Imagine an application that hosts administrative functions at the following URL:
```bash
https://insecure-website.com/administrator-panel-yb556
```
This might not be directly guessable by an attacker. However, the application might still leak the URL to users. The URL might be disclosed in JavaScript that constructs the user interface based on the user's role:
```bash
<script>
	var isAdmin = false;
	if (isAdmin) {
		...
		var adminPanelTag = document.createElement('a');
		adminPanelTag.setAttribute('https://insecure-website.com/administrator-panel-yb556');
		adminPanelTag.innerText = 'Admin panel';
		...
	}
</script>
```
