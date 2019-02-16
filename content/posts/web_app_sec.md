---
title: "Web Application Security - Applying Learning to Practice"
date: 2019-02-15T17:06:56+11:00
author: Cameron Wang
description: The Importance of Learning and Understanding Web Application Security, and its Effects on Businesses and Stakeholders
---
## Problem Statement
In the modern age, the world wide web is one of the most important and popular resources available. 
Millions of users use the world wide web to access web applications, for social media (Facebook, Twitter, Instagram), researching, transactions (Banking, Shopping), or just for entertainment, every day. 
As such, understanding and learning Web Application Security is important to ensure the security and integrity of user data stored in web applications.

## Web Application Vulnerabilities
Currently I have been studying background information of web applications and web technology to gather an understanding of the inner workings of web systems, as well as learning, practicing and understanding the methodology behind web application exploits through multiple resources, 
such as CTFs (RootMe, ShellterLabs, Hacker 101), wargames (OverTheWire Natas), and online practical courses (PentesterLab's Web for Pentester).

Through these resources, I have developed a solid understanding behind XSS and SQLi exploits, packet manipulation and the functionality of Burp Suite, which allows an attacker to intercept and modify the contents of transmitting packets.
	
To locate vulnerable websites, along with following under the guidelines of responsible disclosure, I used bug bounty services Bugcrowd and HackerOne. 
Using what I had learnt from the resources, I tried locating any vulnerabilities, however none of the exploits worked. 
XSS scripts do not get executed, systems are implemented in the website that prevent SQL from being injected, blocking attackers from accessing the website, and packets do not contain anything that could be modified to escalate privilege.

Artefacts:

CTFs / Wargames Write-Ups - https://drive.google.com/drive/u/0/folders/1rZB5U7wRwRWjFeR5LwEwaUf3xFxc1UuL

- Hacker 101
{{<image src="/img/hacker101_ctf.jpg" alt="hacker101 ctf" position="center" style="border-radius: 8px;">}}
	
- OverTheWire Natas
{{<image src="/img/overthewire_natas.jpg" alt="overthewire natas" position="center" style="border-radius: 8px;">}}
	
Web Vulnerability Notes - https://drive.google.com/drive/u/0/folders/1fYNsXDC-b_NBwSqMgLIOEPER_b6Ziwuz

- [ShellterLabs] (https://shellterlabs.com/en/training/get-started/web-application-basics/)
- [PentesterLab - Web for Pentester] (https://www.pentesterlab.com/exercises/web_for_pentester/course)
	- Web Application and Web Technology Notes
	- Web Vulnerabilities
		
Presentation - https://drive.google.com/drive/u/0/folders/15X5fWCr9bx_ILcXTApbRmlDi1Bh2Dzop

## Technical Understanding
### Cross Site Scripting (XSS)
One of the most common, yet most dangerous security threat (#7 in the OWASP Top 10) in Web Applications is Cross Site Scripting (XSS). Although used in conjunction with other vulnerabilities in attacks, XSS allows an attacker to inject arbitrary HTML and JavaScript code into a website, which executes in the web browser of legitimate users. 

XSS exploits can allow attacker to:
- Inject fake login forms
- Retrieving legitimate users' cookies
- Injecting browser exploits
- Getting users to perform arbitrary actions in the web appllication

There are three types of XSS vulnerabilities:
- Stored (Persistent)
	- Stored XSS occurs when injected scripts become permanently stored on the server, such as a database or message forum. Victims then retrieve and execute the malicious script from the server when it requests the stored information.
	- Also referred to as Persistent or Type-I XSS.
- Reflected (Non-Persistent)
	- Reflected XSS occurs when injected scripts are reflected off the web server, such as in an error message, search result, or any other response that includes some or all of the input sent to the server as part of the request. Reflected XSS is delivered to victims through malicious links and sites, or crafted forms, injecting code to the vulnerable website, which reflects the attack back to the user's browser. The browser then executes the code.
	- Also referred to as Non-Persistent or Type-II XSS.
- DOM Based
	- DOM Based XSS occurs by executing payloads as a result from modifying the DOM environemnt in the victim's browser, causing the client side code to execute in an unexpected manner. The malicious modification on the DOM enviornment causes the client side code to execute different, despite the page itself (HTTP response) unchanged.
	- Also referred to as Type-0 XSS.

### SQL Injection (SQLi)
SQL injections are one of the most common web vulnerabilities (#1 in the OWASP Top 10), which stems from a lack of encoding/escaping of user-controlled input of SQL queries. SQL injections can be used to read or modify (Insert/Update/Delete) sensitive data from the database, execute administration operations on the database, recover the content of a file on the Database Management System (DBMS) file system, and can be used to issue commands to the operating system in certain cases.

### Packet Manipulation / Burp Suite
Packets are data containing information that is sent between a client and a web server. Client packets requesting access to the web application, providing information on the host they wish to connect to, the referer, and cookies. Server packets are responses, providing information on the server, and setting cookies. However, if misused, the data sent in packets, such as the cookies, can be easily read and modified by an attacker during transmission, allowing access to privileges and data they would not normally allowed access to.

Burp Suite is a graphical security application used for testing Web Application security. Using the Proxy tool, Burp Suite can listen and intercept packets sent through the proxy, which can be modified before forwarding the packet to its destination.

## The Effects of Web App Sec on Businesses/Stakeholders
It is important for businesses to understand the importance of security for their web applications. Without the proper security measures, vulnerabilities, as simple and basic as they are, can have severe and devastating effects. 
Attackers can gain access to administrative privileges, or view and modify sensitive data stored in databases on the server. 
Accounts can get hijacked and private information can become leaked, which leads to the reputation and trust of businesses and stakeholders damaged.

With injection attacks such as XSS and SQL, using filtering to check and block certain keywords from being inputted, or sanitizing user input so any potential executable characters are not interpreted as executable code. To avoid packet manipulation, cookies in packets should not contain any fields relating to the privilege of the user.

# Bibliography
OWASP 2019, *XSS (Cross Site Scripting) Prevention Cheat Sheet*, viewed 11 Feburary 2019, <https://www.owasp.org/index.php/XSS_(Cross_Site_Scripting)_Prevention_Cheat_Sheet#Why_Can.27t_I_Just_HTML_Entity_Encode_Untrusted_Data.3F>

Wikipedia 2019, *Burp Suite*, viewed 16 Feburary 2019, <https://www.owasp.org/index.php/XSS_(Cross_Site_Scripting)_Prevention_Cheat_Sheet#Why_Can.27t_I_Just_HTML_Entity_Encode_Untrusted_Data.3F>

PentesterLab 2013, *Web for Pentester*, viewed 14 Feburary 2019, <https://www.pentesterlab.com/exercises/web_for_pentester/course>

ShelltherLabs 2019, *Web Application Basics*, viewed 14 Febrary 2019, <https://shellterlabs.com/en/training/get-started/web-application-basics/>
