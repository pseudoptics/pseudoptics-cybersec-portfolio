---
title: "Week 3 - Sprint 3 Reflection"
date: 2019-02-23T01:05:33+11:00
author: Cameron Wang
description: My thoughts and reflections towards my experiences during the third week of the subject. 
---
---

**Week 3 Artefacts** - https://drive.google.com/open?id=1fMzElIGajMD4vWje1Ccxy5-HEGdaTc6V

---

# Sprint Reflection

The third week of this subject has definitely been a fun and interesting experience, understanding the penetration tester mindset and the security tools in-depth, and applying my understanding in practice
through locating and exploiting vulnerabilities in vulnerable virtual machines (as well as a real world web application).

---

The main focus of the third week was **Applying Our Understanding and Learning to Practice**, accomplished through locating and exploiting vulnerabilities to gain root in vulnerable boot2root virtual
machines. Although my knowledge in the field of cyber security has grown throughout the past three weeks of the subject, my skills in security still remain in the beginner range, and as such, the boot2root
virtual machines I attempted were beginner leveled so I can continue to develop my skills through practice. The machines I specifically worked through to gain root were the **'Kioptrix Level 1'** machine,
which I had managed to gain root privileges on, and **'pwnlab_init'** machine, which I have currently not managed to gain root access, and as of writing this reflection, still currently working on gaining
root. Being able to work through the boot2root exercises has provided a lot of experience and knowledge not only on the mindset and tools used for penetration testing machines, but on understanding and
networking virtual machines. To supplement our task, we were assigned a research task on security tools, researching on one or more tools, and understanding in-depth about the purpose of the tool, and how it
functions. My group focused on password cracking tools, such as John the Ripper and Hashcat, allowing us to learn more about passwords, how passwords are stored and encrypted, and how these tools break it at 
a technical level. The other presentations from other groups further expanded my knowledge on the vast tools available, learning about their purpose and applications in penetration testing.
As another option, we were allowed to penetration test the [apointb](https://apointb.com/) web applications, which are real world web application that we were given permission to attack and locate
vulnerabilities. I have attempted to penetrate their applications, looking through their different directories and attempting XSS and SQL Injection, but I was unable to locate any vulnerabilities.

*Artefacts*:

Kioptrix Level 1 Blog Post - https://pseudoptics.me/posts/boot2root_kioptrix_level1/

pwnlab_init Blog Post - https://pseudoptics.me/posts/boot2root_pwnlab_init/

Password Crackers Blog Post - https://pseudoptics.me/posts/password_crackers/

Password Cracking Tools Presentation Slides - https://drive.google.com/open?id=19pyZex1FxaI0cgyVpWVL-kwV0NOk2zfj

Password Cracking Tools Presentation/Research Notes - https://drive.google.com/open?id=143EphJHPWsTkD6uwa90a5gieag-7jXR3

---

On Wednesday (20/02/2019), as a group, we were required to present a high level presentation our research on our chosen security tool/s, discussing what the tools are, how the tools work, and how the tools can be used
to break into complex and vulnerable systems. Working with Brendan Huynh, Thanh Tung Vu and Xiaoke Cui, we focused our presentation on password cracking tools, specifically John the Ripper and Hashcat, describing how
they function, and the repercussions from attacks using these tools in real world situations. I was appointed leader of the group, and although our research on password cracking tools was detailed and in-depth, our
presentation went over the appointed time limit, and provided little amounts of examples and demonstrations of the tools, which may have been caused by my lack of proper time management and leadership as the leader.
I have never been a leader for a group project before this task, so this has definitely been an important experience for me, and I will use what I've learnt to improve myself as a leader for group projects in the future.

*Artefacts*:

Communication

	- Microsoft Office Teams
	- Microsoft Office Planner

{{<slider2 "/week3-group/img/">}}
	
---

The **Free-for-Alls** continued to replace the scrum meetings for this week. On Monday (18/02/2019), I spoke one on one with Vishal Uniyal, who discussed his issues working with Git through the Windows PowerShell.
Instead, he uses GitKraken, which is a Graphical User Interface (GUI) Git client which allows simple and easy pushing, pulling and merging of content through dragging and dropping, as well as other services
which make version control of content simple to manage. As someone who also faces issues working with Git on the command line, GitKraken may be a solution to help upload and update my website contents without
issue. Throughout the weekend, he had focused on his static site, and working through HackTheBox, obtaining the invitation code, and hacking through their machines.

On Friday (22/02/2019), I spoke with Brendan Huynh, Corey Hall, and Harry Louskos, discussing about our progress on our work throughout the week. Corey Hall worked on the 'Bank' boot2root machine, performing
enumeration on the machine through nmap and directory scans, but has currently not gained root. Harry Louskos worked through the Popcorn HackTheBox machine, and Brendan Huynh has been working through HackTheBox
machines, but has been suffering from issues while setting up Virtual Machines through VMware. Virtual Machines are not properly connect to the network, bridged and NAT networking do not work as intended, and
certain virtual machines do not contain the necessary files to properly run. I also face some of the issues that Brendan has been facing with virtual machines, however, currently no solution has been found or
discussed.

*Artefacts*:

Week 3 Free-for-All - https://drive.google.com/open?id=1Xhes54aQ-cgXV8dFlm8bkMjsgr2h9AEG

{{<image src="/img/week3f4a.PNG" alt="week 3 free-for-all" position="center" style="border-radius: 8px;">}}

---

On Wednesday (20/02/2018), security professionals from Deloitte, Viren, Simon and Nathan, visited the class and provided an in-depth presentation on the field of Cyber Security. Focusing specifically on Red Teaming, 
the Deloitte team discussed who they are and what they do, what Red Teams are, how they differ from traditional penetration testers, and the types of tools and methodologies they use when red teaming, providing their
own experiences on the job alongside their presentation to further present the image of the work Red Teams perform. As someone who is considering looking into a career in Cyber Security, the Deloitte team have provided
me with a deep and detailed understanding of the type of work that security professionals do in the field.

*Artefacts*:

Deloitte Presentation Notes - https://drive.google.com/open?id=1YwpA0aKDuLeC6LXYoez6LS0XPLiCFbUL

---

Currently, feedback for my reflections are good. Although I did not receive my feedback for the Wednesday (20/02/2019) presentation, I feel as if I spoke too fast, and the content I presented wasn't substatial enough. This
may be caused from a lack of time management and leadership on my part, and I will aim to resolve these issues for future tasks.

{{<image src="/img/darsh_feedback2.png" alt="darsh feedback" position="center" style="border-radius: 8px;">}}

--- 

Working with VMware, and some of the boot2root Virtual Machines, was the biggest challenge I faced this week. A small hassle I encountered were that certain virtual machines used the NAT network, while other machines were
forced to run using the Bridged network, requiring me understand and constantly switch the network my Kali Linux virtual machine was connected to, so I could work on different boot2root machines. While working through this
weeks task, I discovered that some of the boot2root virtual machines I planned to work through did not work, popping up errors every time they were run on VMware. I believe the issue is caused from certain files missing
from the virtual machine, causing it to start incorrectly, however, no conclusive cause or solution has been found.
