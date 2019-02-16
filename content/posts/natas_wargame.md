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

## natas10 -> natas11
1. View Webpage Source Code
	- Certain Characters are Being Filtered
2. In the Search Bar, Input: ".* /etc/natas_webpass/natas11 #"
	- '\*' is the wildcard character, which locates any character
	- '#' is the comment character, which converts all strings after the character into non-exeutable characters
	- Utilizing the grep command, the command outputs all files and comments out 'dictionary.txt'

## natas11 -> natas12
Cookies are protected using XOR encryption
1. View Webpage Source Code
	- Read the source code to understand the encryption
	- XOR encryption uses a key to encrypt
2. Using Burp Suite, copy the encrypted cookie data
3. Adjust the xor_encryption PHP function to obtain the encryption key
	- Code:
	
"\<?  
$orig_cookie = base64_decode('ClVLIh4ASCsCBE8lAxMacFMZV2hdVVotEhhUJQNVAmhSEV4sFxFeaAw');  
function xor_encrypt($in) {  
  $text = $in;  
  $key = json_encode(array( "showpassword"=>"no", "bgcolor"=>"#ffffff"));  
  $outText = '';  
  // Iterate through each character  
  for($i=0;$i<strlen($text);$i++) {  
  $outText .= $text[$i] ^ $key[$i % strlen($key)];  
  }  
  return $outText;  
}  
print xor_encrypt($orig_cookie);
?\>"

4. Using the key: "qw8j", encrypt a new base64-encoded data cookie, with "showpassword"=>"yes"
	- Code:

function xor_encrypt() {  
  $text = json_encode(array( "showpassword"=>"yes", "bgcolor"=>"#ffffff"));  
  $key = "qw8J";    
  $outText = '';  
  // Iterate through each character  
  for($i=0;$i<strlen($text);$i++) {  
  $outText .= $text[$i] ^ $key[$i % strlen($key)];  
  }  
  return $outText;  
}  
print base64_encode(xor_encrypt());
