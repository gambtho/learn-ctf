---
title: "Enumerating Web Sites"
date: 2017-07-31T21:45:38Z
draft: true
---

# Introduction
Often times networks are accessible through some sort of public web site. One of the keys to successfully gaining a foothold on a network is to enumerate a website and gather more information and find vulnerabilities.

There are a variety of tools to automate the task of enumerating websites. We won't cover all of the tools here in this article but we will cover some of the more popular tools. Additionally, [Nmap](http://learn.greyhatctf.com/attack/nmap/) can also be used to enumerate websites using NSE scripts. 

# robots.txt
robots.txt file is a text file located in the root of the web directory and is designed to notify web crawlers which directories it should not crawl. robots.txt is a publically accessible file and the restriction to crawl pages listed in the file is a directive only. Attackers can just as easily view the robots.txt file and go to the directories listed there.

robots.txt is a great way to quickly check if there are interesting directories on the web server which should be investigated.

Sample robots.txt from https://wordpress.org/
```
User-agent: *
Disallow: /search
Disallow: /support/search.php
Disallow: /extend/plugins/search.php
Disallow: /plugins/search.php
Disallow: /extend/themes/search.php
Disallow: /themes/search.php
Disallow: /support/rss
Disallow: /archive/
```

# DirBuster
DirBuster is a free Java based application that can be used to scan for web site directories. It comes packaged with lists of directories that can be scanned for. The application is multi-threaded and can run very fast on multi-core CPUs. DirBuster is a great way to scan for directories that may not be linked from the homepage or search engines.

Basic Usage:
1. Enter target URL
2. Select word list ![DirBuster Start](/attack/dirbuster_start.png)
3. Click start
4. View results ![DirBuster Results](/attack/dirbuster_results.png)



# Nikto

# WPScan

# References
1. [Category:OWASP DirBuster Project](https://www.owasp.org/index.php/Category:OWASP_DirBuster_Project)
2. [The Web Robots Pages](http://www.robotstxt.org/robotstxt.html)
