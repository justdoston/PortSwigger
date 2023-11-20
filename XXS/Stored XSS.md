# What is stored cross-site scripting?
Stored cross-site scripting (also known as second-order or persistent XSS) arises when an application receives data from an untrusted source and includes that data within its later HTTP responses in an unsafe way.

Suppose a website allows users to submit comments on blog posts, which are displayed to other users. Users submit comments using an HTTP request like the following:
```
POST /post/comment HTTP/1.1
Host: vulnerable-website.com
Content-Length: 100

postId=3&comment=This+post+was+extremely+helpful.&name=Carlos+Montoya&email=carlos%40normal-user.net
```
After this comment has been submitted, any user who visits the blog post will receive the following within the application's response:
```bash
<p>This post was extremely helpful.</p>
```
Assuming the application doesn't perform any other processing of the data, an attacker can submit a malicious comment like this:
```bash
<script>/* Bad stuff here... */</script>
```
Within the attacker's request, this comment would be URL-encoded as:
```bash
comment=%3Cscript%3E%2F*%2BBad%2Bstuff%2Bhere...%2B*%2F%3C%2Fscript%3E
```
Any user who visits receive the following response:
```bash
<p><script>/* Bad stuff here... */</script></p>
```
