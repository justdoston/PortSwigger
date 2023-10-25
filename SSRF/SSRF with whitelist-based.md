# SSRF with whitelist-based input filters

Some applications only allow inputs that match, a whitelist of permitted values. The filter may look for a match at the beginning of the input, or contained within in it.
You may be able to bypass this filter by exploiting inconsistencies in URL parsing.

The URL specification contains a number of features that are likely to be overlooked when URLs implement ad-hoc parsing and validation using this method:

1)You can embed credentials in a URL before the hostname, using the @ character. For example:
```bash
https://expected-host:fakepassword@evil-host
```
2) You can use the `#` character to indicate a URL fragment. For example:
```bash
https://evil-host#expected-host
```
Most important thing we can change url to another for exploit vulnerabilitiy
