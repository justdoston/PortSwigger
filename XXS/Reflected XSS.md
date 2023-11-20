# What is reflected cross-site scripting?

Reflected cross-site scripting (or XSS) arises when an application receives data in an HTTP request and includes that data within the immediate response in an unsafe way.

Suppose a website has a search function which receives the user-supplied search term in a URL parameter:
```bash
https://insecure-website.com/search?term=gift
```
The application echoes the supplied search term in the response to this URL:
```bash
<p>You searched for: gift</p>
```
Assuming the application doesn't perform any other processing of the data, an attacker can construct an attack like this:
```bash
https://insecure-website.com/search?term=<script>/*+Bad+stuff+here...+*/</script>
```
If another user of the application requests the attacker's URL, then the script supplied by the attacker will execute in the victim user's browser, in the context of their session with the application.

# Impact of reflected XSS attacks

If an attacker can control a script that is executed in the victim's browser, then they can typically fully compromise that user. Amongst other things, the attacker can:

1) Perform any action within the application that the user can perform.
2) View any information that the user is able to view.
3) Modify any information that the user is able to modify.
4) Initiate interactions with other application users, including malicious attacks, that will appear to originate from the initial victim user.
