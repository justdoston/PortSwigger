# Common obstacles to exploiting path traversal vulnerabilities

If an application strips or blocks directory traversal sequences from the user-supplied filename, 
it might be possible to bypass the defense using a variety of techniques.

1)You might be able to use an absolute path from the filesystem root, such as `filename=/etc/passwd`, to directly reference a file without using any traversal sequences.
<br>
2) You might be able to use nested traversal sequences, such as `....//` or `....\/`. These revert to simple traversal sequences when the inner sequence is stripped.
<br>
3)An application may require the user-supplied filename to end with an expected file extension, such as `.png`. 
In this case, it might be possible to use a null byte to effectively terminate the file path before the required extension.
```bash
filename=../../../etc/passwd%00.png
```
