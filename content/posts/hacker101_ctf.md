---
title: "CTF - Hacker101"
date: 2019-02-15T22:38:52+11:00
author: Cameron Wang
description: Write-Up of my Hacker101 CTF.
---
## Challenge: A little something to get you started
- Flag 1
	- Checking the source code of the blank page provides a file called "background.png".
	- By redirecting to the file in the server, the webpage displays the flag.

## Challenge: Micro-CMS v1
- Flag 1
	- On the "Testing" page, or when creating a new page, inject a XSS vulnerability into the page without using the **<script>** tag, or without using the word **script**, as it is blacklisted.
	- Using the **<img>** or **<a>** tags can inject a XSS vulnerability.
	- View source code to find the flag in the tag.