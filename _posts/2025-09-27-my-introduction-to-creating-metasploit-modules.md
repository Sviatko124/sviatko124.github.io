---
layout: post
date: 2025-09-27
author: Sviatko124
tags: Metasploit-Framework
---
In this blog post, I briefly explain my introduction to developing exploit modules in Ruby with the Metasploit Framework. 
I felt like I relied too much on Metasploit modules without fully even understanding how they're written, so to change that, I set out to create my own simple exploit module. 
All source code for my target program and exploit module are available here:
[https://github.com/Sviatko124/metasploit-challenge-project]
Note: I'm aware that I didn't use a built-in Metasploit payload and handler. I really tried, but with limited resources and tutorials available, I was only able to create a basic interactive shell. I hope to return to this project in the future and figure this part out someday. 

Disclaimer: Do not expose my vulnerable C program to any untrusted networks, as it is trivial to exploit. You have been warned. 

## The Goal
My goal for this project was to challenge myself to create an exploit module in Ruby for the Metasploit Framework. This would help me understand the real exploit modules I will use in the future more clearly and make me appreciate the existing exploit developers for their knowledge and skills. 

## Target Program
To create an exploit module, you need a service to exploit. I knew I would have to use C for low-level control over adding my own vulnerabilities (in the future, I'm hoping to expand on this project and learn to exploit the segmentation fault vulnerability to achieve RCE). 
I was able to program the target service relatively quickly, and I decided to make my service simply print the local system date and time. I thought a nice way to include a CLI vulnerability would be to ask the user's name and use their name value inside an echo command, which would obviously allow for an easy command execution. 

## The Exploit Module
Since I didn't know even a little bit of Ruby, I started off with the Ruby quickstart guide, which taught me the language basics:
[https://www.ruby-lang.org/en/documentation/quickstart]

To get an introduction to the general structure of a Metasploit module, I checked the following guide:
[https://www.offsec.com/metasploit-unleashed/building-module/]

Other than that, I occasionally had to search for various things on the web, like how to make my command input/output part of the program. Luckily, I noticed similarities between Ruby's socket library and Python's socket library, and I could finish this part of the program more easily. I also *borrowed* some code from existing Metasploit modules. 

## All Together and Conclusions
It was great to see my project come to fruition. I learned a lot about Metasploit modules, and although I only learned surface-level information, I felt like I could already read module code a lot better and understand everything that's happening in them. 
Although this was a great introduction, I don't have much time to dedicate to this project as I am busy with high school, but someday I hope to learn about handlers, generating my own Metasploit payloads, and exploit the buffer overflow vulnerability in my program. 

Hope you found my journey helpful, have a good day! 
