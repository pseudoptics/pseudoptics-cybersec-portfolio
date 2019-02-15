---
title: "Wargames - OverTheWire Natas"
date: 2019-02-15T22:41:32+11:00
author: Cameron Wang
description: Write-Up of my OverTheWire Natas wargame.
---
## natas0 -> natas1
- View Page Source

## natas 1 -> natas2
- View Page Source (using shortcut: fn + f12)

## natas2 -> natas3
1. View Page Source
2. Go To: /files
3. View 'users.txt'

## natas3 -> natas4
1. View: /robots.txt
2. Go To: /s3cr3ts
3. View 'users.txt'

## natas4 -> natas5
1. Use Burp Suite to intercept Packet
2. Locate Referer in Packet
3. Modify Referer To: http://natas5.natas.labs.overthewire.org/

## natas5 -> natas6
1. Use Burp Suite to intercept Packet
2. Locate Cookie in Packet
3. Modify loggedin=0 To: loggedin=1

## natas6 -> natas7
1. View Webpage Source Code
2. Go To: /includes/secret.inc
3. View Page Source
4. Input Secret Hidden in Page Source

## natas7 -> natas8
1. View Page Source
2. Enter Password Directory Location in the PHP in the URL
	- index.php?page=/etc/natas_webpass/natas8

## natas8 -> natas9
1. View Webpage Source Code
2. Convert encoded string: "3d3d516343746d4d6d6c315669563362" from Hexadecimal to ASCII
3. Reverse ASCII String: "==QcCtmMml1ViV3b"
4. Decode Base64 String: "b3ViV1lmMmtCcQ=="
5. Input Secret: "oubWYf2kBq"

## natas9 -> natas10
1. View Webpage Source Code
2. In the Search Bar, Enter Unix Commands
	- When using the passthru() function, inputs are not properly sanitized, allowing input commands to be executed.
3. Input: "/etc/natas_webpass/natas10"
