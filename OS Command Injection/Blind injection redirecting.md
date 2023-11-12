# Exploiting blind OS command injection by redirecting output

You can redirect the output from the injected command into a file within the web root that you can then retrieve using the browser. For example, if the application serves static resources from the filesystem location `/var/www/static`, then you can submit the following input:
