# Preventing file execution in user-accessible directories

While it's clearly better to prevent dangerous file types being uploaded in the first place, the second line of defense is to stop the server from executing any scripts that do slip through the net.

As a precaution, servers generally only run scripts whose MIME type they have been explicitly configured to execute. Otherwise, they may just return some kind of error message or, in some cases, serve the contents of the file as plain text instead:

```
GET /static/exploit.php?command=id HTTP/1.1
Host: normal-website.com


HTTP/1.1 200 OK
Content-Type: text/plain
Content-Length: 39

<?php echo system($_GET['command']); ?>
```

This kind of configuration often differs between directories. A directory to which user-supplied files are uploaded will likely have much stricter controls than other locations on the filesystem that are assumed to be out of reach for end users. If you can find a way to upload a script to a different directory that's not supposed to contain user-supplied files, the server may execute your script after all.

Web servers often use the `filename` field in `multipart/form-data` requests to determine the name and location where the file should be saved.


# Lab traversal

1) Tried to upload web shell
2) In burp suite we captured request like: `Content-Disposition: form-data; name="avatar"; filename="exploit.php"`<br> In it's name I tried to change `../exploit.php` meaning file uploading to another folder to launch
3) And.. we can confirm by browsing location

Good explanation on you tube:
https://youtu.be/7mISCBhwcXM
