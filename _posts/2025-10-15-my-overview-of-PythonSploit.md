---
layout: post
date: 2025-10-15
author: Sviatko124
tags: Python PythonSploit
---
In this blog post, I cover my journey on how I created the first version of PythonSploit, a Meterpreter-inspired tool designed to help make my workflow more efficient during CTFs. 

I will present a high-level overview of my program and introduce future features I will try to add that will help improve my project. 

The project discussed in this post is available at: [https://github.com/Sviatko124/PythonSploit](https://github.com/Sviatko124/PythonSploit)

Disclaimer: Please use this tool ethically. I do not take any responsibility for how you use this tool. This tool is intended to be primarily used in CTFs.
Also, I only tested this tool locally. If you find any bugs, feel free to make an issue on the project page. 

## Overview
PythonSploit is a modular Python listener and handler system that can manage multiple concurrent connections and give each one an interactive, user-friendly session interface. Everything runs in Python, without external frameworks or dependencies beyond rich for styling. 

The main feature of the program is that it manages a background-threaded listener accepting multiple concurrent sessions. At start-up, the program initializes a background listener on an available port. When a connection to the port is established by a client, the program assigns a unique ID for the session and appends it to a list variable, where the session can be put in background and accessed later. Programming a threaded listener was initially a buggy headache to implement as I wasn't experienced with threading, but luckily, Python makes it a lot easier. I found that I can utilize thread locks to only let one change to a thread process occur at once, so that I wouldn't run into race conditions. 

For the method of interaction with each session, I drew a lot of inspiration from the Meterpreter handler within the Metasploit Framework. This is evident in the design of the `interact` command in the console, which lists each session ID and basic information related to that session, like the user who was compromised in that session. Another part of the Meterpreter handler I implemented was session commands like \upload, \download, and \bg. Uploading and downloading files is a common task needed in a CTF challenge, but it is often very bothersome in practice, so this feature is incredibly helpful. My method of implementing file transfers is to base64 encode the local file, and append it to a remote file via a direct echo command, and decoding it at the destination. Although I considered this method crude, I figured since it worked well, I probably didn't need to change it. 

The final idea I borrowed from the Metasploit Framework was to create a reverse shell generator inside the program. This was relatively trivial to implement, I borrowed some common reverse shells from (https://revshells.com), and made the program fill in the listener IP and PORT for the user, so all the user has to do is copy-paste and run the payload into their non-interactive shell. 

Finally, I wanted to make the program look visually appealing. This was easily achieved with the rich Python library, and after importing it I customized the text colors in my program to my heart's content. I also generated a cool ASCII logo for the program that shows up on each start-up. I also decided to make more graceful user exits (so Ctrl + C won't crash the program but instead exit it properly). I mainly did this to help the project feel more professional. 


## To-do
Currently, the program only supports Linux targets. This is usually enough for most CTFs or HTB boxes, but especially in HTB, Windows targets are pretty common. Therefore, whenever I get the chance I will try to add support for Windows targets. 
Note, I won't attempt to add AV bypass, as in CTFs and HTB the antivirus is commonly disabled, and I don't want to give people the opportunity to use my program for evil. 

Additionally, I would like to add more session commands. I haven't thought what I would add, but as I'm writing it I'm considering terminal macros like establishing persistance, or to quickly gather basic system information, or perhaps a macro that can perform quick "easy win" checks for privilege escalation. 


Hope you enjoy using my project, and have a great day! 
