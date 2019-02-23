---
title: "boot2root - Kioptrix Level 1"
date: 2019-02-21T19:44:05+11:00
author: Cameron Wang
description: My Steps/Process of Gaining Root on the Kioptrix Level 1 Machine
---

'boot2root - Kioptrix Level 1' Notes - https://drive.google.com/open?id=1ELx9NS0ONeKRIN5NSrjgSSxfMo-Pl8VN

---
# Kioptrix Level 1 - Rooted
## Gaining Root
Walkthrough of the Process:

First, I need to locate the IP Address of the vulnerable machine I am attacking. This can be accomplished through the `nmap -sP [IP Address]` command, which sends a ping out to all machines connected on the network and waits for a response. Using `netdiscover -i eth0 -r [IP Address]` also completes the same task.
		
{{<image src="/img/netdiscover.PNG" alt="netdiscover" position="center" style="border-radius: 8px;">}}
	
	- Kioptrix IP Address: 192.168.43.115
		
Once I have obtained the IP Address of the machine I want to attack, I next have to scan for all the ports on the machine, which can be done using the command `nmap -sSV -n -T4 -p 1-5000 [IP Address]`. Using the option `-sSV` returns the versions of the services that the machine is running. Knowning the versions of each service running can help locate exploits which can be used to gain root on the machine.

{{<image src="/img/nmap.PNG" alt="nmap" position="center" style="border-radius: 8px;">}}

Checking out the website at the machine's IP Address directs us to an Apache Test Webpage. Doesn't seem like anything can be accomplished on the website itself.

{{<image src="/img/testpage.PNG" alt="test page" position="center" style="border-radius: 8px;">}}

Using the command `searchsploit [service]`, I can look through the Exploit-DB database to locate any exploits for the services currently running on the machine. mod_ssl has an exlpoit that could be useful for me.

{{<image src="/img/searchsploit.PNG" alt="searchsploit" position="center" style="border-radius: 8px;">}}

	- Exploit Used: Apache mod_ssl < 2.8.7 OpenSSL - 'OpenFuckV2.c' Remote Buffer Overflow
		- URL: https://www.exploit-db.com/exploits/76
		
I can download the exploit from either the website itself, or using the command `wget [URL]` to download the raw code of the exploit. Following the instructions in the program, I try using the GCC compiler, but the program does not compile due to various errors in the code. Following a guide, I have modified the code using the command `vim [file]` so it will properly compile and run.

{{<image src="/img/vim_764.PNG" alt="vim 764.c" position="center" style="border-radius: 8px;">}}

	- Guide Used To Compile: https://medium.com/@javarmutt/how-to-compile-openfuckv2-c-69e457b4a1d1
	
Running `./OpenFuck` allows me to read the instructions and understand how to use it. The machine I am attacking is running RedHat Linux 7.2 (apache-1.3.20-16)2 (0x6b), so using the command `./OpenFuck 0x6b 192.168.43.115 443 -c 50`, the program exploits the vulnerability and runs a remote shell on the machine. Using the command `whoami`, I can check to see what user I am running at. In this case, I have gained root onto the machine.
# Machine Rooted

{{<image src="/img/openfuck.PNG" alt="OpenFuckV2" position="center" style="border-radius: 8px;">}}
{{<image src="/img/whoami.PNG" alt="root" position="center" style="border-radius: 8px;">}}
