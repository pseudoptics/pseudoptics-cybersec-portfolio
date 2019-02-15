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

One of the most common, yet most dangerous security threat (#7 in the OWASP Top 10) in Web Applications is Cross Site Scripting (XSS). 
Although used in conjunction with other vulnerabilities in attacks, XSS allows an attacker to inject code into the website. 
SQL Injection is also another common and severe flaw (#1 in the OWASP Top 10), where SQL code can be injected to queries to either echo back data from databases, or bypass login screens. 
By reading and modifying the data sent in packets, such as the cookies, an attacker can gain access to privileges and data they would not normally allowed access to.

Artefacts:
- CTFs / Wargames: https://drive.google.com/drive/u/0/folders/1rZB5U7wRwRWjFeR5LwEwaUf3xFxc1UuL
	- Hacker 101
	- OverTheWire Natas
- Web Vulnerability Notes: https://drive.google.com/drive/u/0/folders/1fYNsXDC-b_NBwSqMgLIOEPER_b6Ziwuz
	- ShellterLabs
	- PentesterLab - Web for Pentester
		- Web Application and Web Technology Notes
		- Web Vulnerabilities
- Presentation: https://drive.google.com/drive/u/0/folders/15X5fWCr9bx_ILcXTApbRmlDi1Bh2Dzop
	
To locate vulnerable websites, along with following under the guidelines of responsible disclosure, I used bug bounty services Bugcrowd and HackerOne. 
Using what I had learnt from the resources, I tried locating any vulnerabilities, however none of the exploits worked. 
XSS scripts do not get executed, systems are implemented in the website that prevent SQL from being injected, blocking attackers from accessing the website, and packets do not contain anything that could be modified to escalate privilege.

## The Effects of Web App Sec on Businesses/Stakeholders
It is important for businesses to understand the importance of security for their web applications. Without the proper security measures, vulnerabilities, as simple and basic as they are, can have severe and devastating effects. 
Attackers can gain access to administrative privileges, or view and modify sensitive data stored in databases on the server. 
Accounts can get hijacked and private information can become leaked, which leads to the reputation and trust of businesses and stakeholders damaged.

With injection attacks such as XSS and SQL, using filtering to check and block certain keywords from being inputted, or sanitizing user input so any potential executable characters are not interpreted as executable code.