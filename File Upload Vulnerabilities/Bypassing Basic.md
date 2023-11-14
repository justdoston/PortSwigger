# Lab
1) First of all attempt to upload malicious php file: `<?php echo file_get_contents('/home/carlos/secret'); ?>`
2) Notice, we are not allowed because of `Content-Type`
3) Send request to `burp repeater` change `Content-Type` to `image/jpeg`.
4) After uploading just browse accoring to file name\

Explanation from you tube:
https://youtu.be/QHhn0-ermck
