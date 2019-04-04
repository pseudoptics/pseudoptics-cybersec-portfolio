---
title: "Wargames - OverTheWire Bandit"
date: 2019-04-04T22:10:32+11:00
author: Cameron Wang
description: Write-Up of my OverTheWire Bandit wargame **Last Updated 4/04/2019**.
---
## bandit0
SSH (Secure Shell)
- Use SSH with username ```bandit0``` and password ```bandit0``` to SSH onto ```bandit.labs.overthewire.org on Port 2220```.
- Command: ```~# ssh username@host -p port```
	- ```~# ssh bandit0@bandit.labs.overthewire.org -p 2220```

## bandit0 -> bandit1
The ```ls``` and ```cat``` Commands
- Use ```ls``` to list all files in the home directory, and ```cat``` to read the 'readme' text file for the password.
- Command: ```~# ls```
- Command: ```~# cat [filename]```
	- ```~# cat readme```

## bandit1 -> bandit2
Special Characters
- Prepending ```./``` to special characters will cause the console to treat the special character as a regular character.
- Prepend ```./``` to ```-``` to ```cat``` the file and read its contents.
- Command: ```~# cat ./[special character]```
	- ```~# cat ./-```

## bandit2 -> bandit3
Spaces
- Prepending ```\``` to spaces so spaces aren't treated as special characters on the console.
- Prepend ```\``` to the spaces in filename ```spaces in this filename``` to ```cat``` the file and read its contents.
- Command: ```~# cat [file\ name]```
	- ```~# cat spaces\ in\ this\ filename```

## bandit3 -> bandit4
Hidden Files
- Files prepended with .the character ```.``` will be hidden and can't be listed using default ```ls```.
- Using the option ```a``` will reveal all files, including hidden files.
- ```cat``` the hidden file for the password.
- Command: ```~# ls -a```

## bandit4 -> bandit5
The ```file``` Command
- Using the ```file``` command on a file outputs the type of file it is.
- Use ```file``` on each file to locate the ASCII Text file, and ```cat``` the file to read its contents.
- Command: ```~# file [file]```
	- ```~# file ./-file07```

## bandit5 -> bandit6
The ```find``` Command 1
- Using the ```find``` command on a directory, and providing the proper parameters, will output the files whose characteristics fit the parameters.
- ```-size``` checks if files fit the provided size, and ```-readable``` checks if the file can be read in ASCII Text.
- Use ```find``` with the parameters ```-size 1033c``` and ```-readable``` to locate the file that contains the password.
- Command: ```~# find [directory] [parameters]```
	- ```~# find inhere -size 1033c -readable```

## bandit6 -> bandit7
The ```find``` Command 2
- Use the parameters ```-user``` and ```-group``` alongside ```-size``` with the command ```find``` to locate the ```bandit7.password``` file, which contains the password for the next challenge.
- Command: ```~# find [directory] [parameters]```
	- ```~# find / -size 33c -user bandit7 -group bandit6```
