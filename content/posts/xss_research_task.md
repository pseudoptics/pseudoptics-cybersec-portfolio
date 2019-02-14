---
title: "XSS Research Task"
date: 2019-02-14T15:07:02+11:00
author: Cameron Wang
description: Research Task on XSS Vulnerabilities.
---
# Stored XSS Vulnerability
## eBay Stored XSS Vulnerability (2017)
In 2017, eBay suffered from a stored XSS vulnerability exploited by hackers, allowing the attackers to inject malicious JavaScript code into auction descriptions to steal account credentials. Many of the listings with the exploited vulnerability remained on the website for months before being removed. The attackers used malicious scripts on a variety of lower-valued items, including legitimate listings posted from reputable accounts that they had compromised.

The main attack was a phishing attack, which misdirects users into providing their account credentials to the attackers. The XSS attack was used as a tool to redirect unsuspecting users who were visiting product listings to a spoofed form, disguised as an eBay login page, which would transmit the entered data to a script at the URL: "daviddouglas.co.uk/session.php?/ws/eBayISAPI.dll?co_partnerId=2&siteid=3&UsingSSL=1", when the account details (username and password) are submitted. The PHP script then immediately redirects back to the genuine eBay website, providing the impression that the listing they were visiting no longer exists.

As a method to misdirect and avoid any content filters, the script was purposely obfuscated, splitting the URL string into multiple variable. The script present on the listings actually led to a much larger JavaScript payload from an external location at URL: "user54631.vs.easily.co.uk/v.js", hosted on Easily. The external script redirected to the phishing form, which was crafted through a data URI encoded in base64, as an extra level of difficulty for users to report, as the page is technically not hosted anywhere.

## Solutions to Mitigate Stored XSS Vulnerabilities
One of the simplest and common methods to mitigate XSS vulnerabilities is through **filtering**, by checking and removing or blocking certain keywords from being injected into the website. Sanitizing user input is another common method, which essentially scrubs the data clean from potential executable characters, changing user inputs into acceptable data that will not be interpreted as executable code. 

# Bibliography
Netcraft 2017, *Hackers still exploiting eBay's stored XSS vulnerabilities in 2017*, Paul Mutton, viewed 13/02/2019, <https://news.netcraft.com/archives/2017/02/17/hackers-still-exploiting-ebays-stored-xss-vulnerabilities-in-2017.html>

OWASP 2018, *XSS (Cross Site Scripting) Prevention Cheat Sheet*, Jeff Williams, viewed 13/02/2019, <https://www.owasp.org/index.php/XSS_(Cross_Site_Scripting)_Prevention_Cheat_Sheet>

TechTarget 2018, *What is cross-site scripting (XSS)?*, Margaret Rouse, viewed 14/02/2019, <https://searchsecurity.techtarget.com/definition/cross-site-scripting>
