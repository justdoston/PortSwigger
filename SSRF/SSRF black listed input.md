# SSRF with blacklist-based input filters

Some applications block input containing hostnames like `127.0.0.1` and `localhost`, or sensitive URLs like `/admin`. 
In this situation, you can often circumvent the filter using the following techniques:

## 1) 
Use an alternative IP representation of `127.0.0.1`, such as `2130706433`, `017700000001`, or `127.1`.
<br>
## 2)
Register your own domain name that resolves to `127.0.0.1`. You can use `spoofed.burpcollaborator.net` for this purpose.
<br>
## 3)
Obfuscate blocked strings using URL encoding or case variation.
<br>
## 4)
Provide a URL that you control, which redirects to the target URL. 
Try using different redirect codes, as well as different protocols for the target URL. 
For example, switching from an http: to https: URL during the redirect has been shown to bypass some anti-SSRF filters.
