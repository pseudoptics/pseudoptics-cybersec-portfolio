---
title: "boot2root - pwnlab_init"
date: 2019-02-22T17:48:26+11:00
author: Cameron Wang
description: My Steps/Process To Gaining Root on the pwnlab_init Machine 
---
---

'boot2root - pwnlab_init' Notes - https://drive.google.com/open?id=1NJi0w5l3AW3Xb91EdvPl9-tgH1AyJxdi

---
# pwnlab_init - Progressing
## Current Process To Gaining Root

---

**NOTE**: this post will continue to update as I progress with the challenge.

---

Walkthrough of the Process:

First, I need to locate the IP Address of the vulnerable machine I am attacking. This can be accomplished through the `nmap -sP [IP Address]` command, which sends a ping out to all machines connected on the network
and waits for a response. Using `netdiscover -i eth0 -r [IP Address]` also completes the same task.

	- pwnlab_init IP Address: 192.168.43.21
	
{{<image src="/img/pwnlab_netdiscover.PNG" alt="netdiscover" position="center" style="border-radius: 8px;">}}
	
Once I have obtained the IP Address of the machine I want to attack, I next have to scan for all the ports on the machine, which can be done using the command `nmap -sSV -n -T4 -p 1-5000 [IP Address]`.
Using the option `-sSV` returns the versions of the services that the machine is running. Knowning the versions of each service running can help locate exploits which can be used to gain root on the machine.

{{<image src="/img/pwnlab_nmap.PNG" alt="nmap" position="center" style="border-radius: 8px;">}}

Using the command `searchsploit [service]`, I can look through the Exploit-DB database to locate any exploits for the services currently running on the machine. However, it seems that there are no exploits that I
can utilise. The MySQL exploits looked interesting, used to escalate privileges, however it only works locally. It may be useful at a later stage.

{{<image src="/img/pwnlab_searchsploit.PNG" alt="searchsploit" position="center" style="border-radius: 8px;">}}

Checking out the website at the machine's IP Address directs me to a website with a homepage, a login page for administrators, and an upload page, which only allows administrators to upload images onto their
servers.

{{<image src="/img/pwnlab_website.PNG" alt="webpage" position="center" style="border-radius: 8px;">}}
{{<image src="/img/pwnlab_login.PNG" alt="login" position="center" style="border-radius: 8px;">}}
{{<image src="/img/pwnlab_upload.PNG" alt="upload" position="center" style="border-radius: 8px;">}}

The website does not contain a robots.txt file, and the source code for each of the webpages do not seem to contain anything of interest.

{{<image src="/img/robots.PNG" alt="robots.txt" position="center" style="border-radius: 8px;">}}
{{<image src="/img/source.PNG" alt="source code" position="center" style="border-radius: 8px;">}}

Using the command `dirb [URL] /usr/share/wordlists/dirb/common.txt`, or `nikto -h [IP Address]`, I am able to scan for all common directories stored in the web server. However, all of the pages I have visited do
not seem to contain anything of interest.

{{<image src="/img/dirb.PNG" alt="dirb" position="center" style="border-radius: 8px;">}}

On the login page, I have tried performing SQL Injection to bypass the login screen, however, it does not seem like the web application is vulnerable to SQL Injection attacks.

{{<image src="/img/sql1.PNG" alt="sql1" position="center" style="border-radius: 8px;">}}
{{<image src="/img/sql2.PNG" alt="sql2" position="center" style="border-radius: 8px;">}}

Viewing the packets sent to the web application using **Burp Suite**, the cookie contains a header called `PHPSESSID`, which I may be able to manipulate to gain administrator access.

{{<image src="/img/burp.PNG" alt="burp suite" position="center" style="border-radius: 8px;">}}

---

**NOTE**: this post will continue to update as I progress with the challenge.

---
