# Unprotected functionality

At its most basic, vertical privilege escalation arises where an application does not enforce any protection for sensitive functionality.
For example, administrative functions might be linked from an administrator's welcome page but not from a user's welcome page.

For example, a website might host sensitive functionality at the following URL:
```bash
https://insecure-website.com/admin
```
Even if the URL isn't disclosed anywhere, an attacker may be able to use a wordlist to brute-force the location of the sensitive functionality.
