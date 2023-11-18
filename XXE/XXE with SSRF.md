# XXE attack with SSRF
To exploit an XXE vulnerability to perform an [SSRF attack](https://portswigger.net/web-security/ssrf), you need to define an external XML entity using the URL that you want to target, and use the defined entity within a data value.
