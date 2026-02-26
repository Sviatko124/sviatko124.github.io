---
layout: post
date: 2026-02-26
author: Sviatko124
title: "Building a Linux Antivirus in C and Python"
tags: Python C Antivirus
---
Welcome to another one of my blog posts! In this entry, I’m introducing my new project the nature of which I feel is very important in today's computing landscape. Around October 2025, Windows 10 reached end-of-life (EoL), meaning it no longer receives security patches. This means that any new vulnerabilities found in Windows 10 would remain unfixed and leave people exposed. Together with other security concerns regarding Windows 11, many people began exploring Linux. I believe this is a good thing as people are becoming aware of and engaged with the technology they rely on daily. 

However, as more people begin using Linux, it will progressively become a more attractive target for cybercriminals. In the past, Linux malware was quite rare because of its smaller desktop market share and technically experienced user base. Today, the barrier to entry is lower, bringing in a broader range of users, a majority of which having lower security awareness. This change increases the likelihood of social engineering and user-targeted attacks, making proactive security considerations more important than ever. 

For these reasons, I’ve decided to begin a new hobby project: developing a Linux antivirus prototype. While solutions such as ClamAV exist, there is still very little usage of Linux antiviruses in gereral. My goal is not only to learn and experiment with detection techniques, but also to explore how antivirus can be designed without unnecessarily expanding a system’s attack surface, which is one of the key concerns in current Linux antivirus. Through this project, I hope to encourage thoughtful discussion about practical defensive strategies for a growing Linux user base, and take my own shot at creating a Linux antivirus.

The project discussed in this blog is at: [https://github.com/Sviatko124/linux_antivirus](https://github.com/Sviatko124/linux_antivirus)

## Overview

There are two parts to this project: the CLI antivirus tool and it's C modules dependency, and the standalone Python systemd service. There wasn't any particularly good reason to split the project into these two mini-projects, other than the fact that I felt like it :). 

The start of the project was at the CLI python script, which was supposed to contain all the logic for scanning, hasing, detection, and monitoring. I quickly realized that Python by itself was too slow for my purposes, so I decided to try making a C modules library. My idea was that I could code the high level logic in Python, but when it came to needing to recursively compute large directories of files, I would write functions in C to let me do it efficiently. This would allow anybody to easily change the code of the python script to their needs, without having to mess with C. 

Something I learned along the way that I believe a lot of people will benefit from is the existance of the POSIX API function nftw() in C. In essence, it recursively traverses a directory tree, and calls a callback function for every file it discovers. This is incredibly useful as it makes life easier, and I highly recommend using it in your next project!

Anyways, later into the project I decided to expand the project scope, and created the systemd service. It uses solely one python file, but that's because it used my old Python script prototype and I didn't feel like changing it. This segment of the project was more about learning system and creating safe install/uninstall bash scripts, not the service itself. 

## Conclusion

In conclusion, I've learned a lot through the project:
- Python and C integration
- POSIX API and the nftw() function
- Linux filesystem monitoring
- systemd services
- malware signature detection

Although I'm happy about the project, I know there's room for improvement. In the future I wish to implement heuristic detection, and flagging suspicious behaviors from binaries like netcat and such. 

I hope this post was of great value to you and that you find my project useful, and don't forget the project is under the MIT license so you can use any part of it for yourself as long as you credit me. 

Have a great day! 
