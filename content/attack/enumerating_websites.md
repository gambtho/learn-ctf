---
title: "Enumerating Web Sites"
date: 2017-07-04T02:55:11Z
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

## Basic Usage

1. Enter target URL
2. Select word list
3. Click start
4. View results

![DirBuster Start](/attack/dirbuster_start.png)

![DirBuster Results](/attack/dirbuster_results.png)

# Nikto
Nikto is another free and open source web server scanner. Nikto can automatically scan for vulnerabilities on different server types and different content management systems (CMS).

## Basic Usage
```
nikto -host http://192.168.222.159/dvwa/
```

### Output from DVWA
```
- Nikto v2.1.6
---------------------------------------------------------------------------
+ Target IP:          192.168.222.159
+ Target Hostname:    192.168.222.159
+ Target Port:        80
+ Start Time:         2017-07-05 21:00:45 (GMT-4)
---------------------------------------------------------------------------
+ Server: Apache/2.2.8 (Ubuntu) DAV/2
+ Retrieved x-powered-by header: PHP/5.2.4-2ubuntu5.10
+ The anti-clickjacking X-Frame-Options header is not present.
+ The X-XSS-Protection header is not defined. This header can hint to the user agent to protect against some forms of XSS
+ The X-Content-Type-Options header is not set. This could allow the user agent to render the content of the site in a different fashion to the MIME type
+ Cookie PHPSESSID created without the httponly flag
+ Cookie security created without the httponly flag
+ Root page / redirects to: login.php
+ No CGI Directories found (use '-C all' to force check all possible dirs)
+ Server leaks inodes via ETags, header found with file /dvwa/robots.txt, inode: 93164, size: 26, mtime: Tue Mar 16 01:56:22 2010
+ Uncommon header 'tcn' found, with contents: list
+ Apache mod_negotiation is enabled with MultiViews, which allows attackers to easily brute force file names. See http://www.wisec.it/sectou.php?id=4698ebdc59d15. The following alternatives for 'index' were found: index.php
+ Apache/2.2.8 appears to be outdated (current is at least Apache/2.4.12). Apache 2.0.65 (final release) and 2.2.29 are also current.
+ Allowed HTTP Methods: GET, HEAD, POST, OPTIONS, TRACE 
+ OSVDB-877: HTTP TRACE method is active, suggesting the host is vulnerable to XST
+ OSVDB-3268: /dvwa/config/: Directory indexing found.
+ /dvwa/config/: Configuration information may be available remotely.
+ OSVDB-12184: /dvwa/?=PHPB8B5F2A0-3C92-11d3-A3A9-4C7B08C10000: PHP reveals potentially sensitive information via certain HTTP requests that contain specific QUERY strings.
+ OSVDB-12184: /dvwa/?=PHPE9568F36-D428-11d2-A769-00AA001ACF42: PHP reveals potentially sensitive information via certain HTTP requests that contain specific QUERY strings.
+ OSVDB-12184: /dvwa/?=PHPE9568F34-D428-11d2-A769-00AA001ACF42: PHP reveals potentially sensitive information via certain HTTP requests that contain specific QUERY strings.
+ OSVDB-12184: /dvwa/?=PHPE9568F35-D428-11d2-A769-00AA001ACF42: PHP reveals potentially sensitive information via certain HTTP requests that contain specific QUERY strings.
+ OSVDB-3092: /dvwa/login/: This might be interesting...
+ OSVDB-3268: /dvwa/docs/: Directory indexing found.
+ OSVDB-3092: /dvwa/CHANGELOG.txt: A changelog was found.
+ /dvwa/login.php: Admin login page/section found.
+ /dvwa/?-s: PHP allows retrieval of the source code via the -s parameter, and may allow command execution. See http://www.kb.cert.org/vuls/id/520827
+ /dvwa/login.php?-s: PHP allows retrieval of the source code via the -s parameter, and may allow command execution. See http://www.kb.cert.org/vuls/id/520827
+ /dvwa/CHANGELOG.txt: Version number implies that there is a SQL Injection in Drupal 7, can be used for authentication bypass (Drupageddon: see https://www.sektioneins.de/advisories/advisory-012014-drupal-pre-auth-sql-injection-vulnerability.html).
+ 7534 requests: 0 error(s) and 25 item(s) reported on remote host
+ End Time:           2017-07-05 21:00:58 (GMT-4) (13 seconds)
---------------------------------------------------------------------------
+ 1 host(s) tested
```

# WPScan
WordPress is a popular open source CMS. W3Techs reports that WordPress is used on approximately 28% of all websites and 59% of all CMSs. Over the years WordPress has been proven to have many security vulnerabilities. Because of it's popularity and numerous vulnerabilities, it's a wonderful thing when an attacker finds a site powered by WordPress. 

WPScan is free scanner that works specifically with WordPress sites. It can automatically enumerate WordPress sites for vulnerabilities, enumerate users, and attempt to brute force logins.

## Basic Usage Examples

Update database
```
wpscan --update
```

Basic scan
```
wpscan -u http://192.168.222.166/
```

Enumerate users
```
wpscan -u http://192.168.222.166/ -e u
```

Attempt to guess login for user with password list
```
wpscan -u http://192.168.222.166/ --wordlist /usr/share/john/password.lst --username user
```

### Output from standard scan of Bitnami WordPress Stack
```
_______________________________________________________________
        __          _______   _____                  
        \ \        / /  __ \ / ____|                 
         \ \  /\  / /| |__) | (___   ___  __ _ _ __ ®
          \ \/  \/ / |  ___/ \___ \ / __|/ _` | '_ \ 
           \  /\  /  | |     ____) | (__| (_| | | | |
            \/  \/   |_|    |_____/ \___|\__,_|_| |_|

        WordPress Security Scanner by the WPScan Team 
                       Version 2.9.2
          Sponsored by Sucuri - https://sucuri.net
   @_WPScan_, @ethicalhack3r, @erwan_lr, pvdl, @_FireFart_
_______________________________________________________________

[+] URL: http://192.168.222.166/
[+] Started: Wed Jul  5 21:56:06 2017

[+] robots.txt available under: 'http://192.168.222.166/robots.txt'
[+] Interesting entry from robots.txt: http://192.168.222.166/wp-admin/admin-ajax.php
[!] The WordPress 'http://192.168.222.166/readme.html' file exists exposing a version number
[+] Interesting header: LINK: <http://192.168.222.166/wp-json/>; rel="https://api.w.org/"
[+] Interesting header: SERVER: Apache
[+] Interesting header: X-FRAME-OPTIONS: SAMEORIGIN
[+] Interesting header: X-POWERED-BY: PHP/7.0.18
[+] XML-RPC Interface available under: http://192.168.222.166/xmlrpc.php

[+] WordPress version 4.8 (Released on 2017-06-08) identified from meta generator, links opml

[+] WordPress theme in use: twentyseventeen - v1.3

[+] Name: twentyseventeen - v1.3
 |  Latest version: 1.3 (up to date)
 |  Location: http://192.168.222.166/wp-content/themes/twentyseventeen/
 |  Readme: http://192.168.222.166/wp-content/themes/twentyseventeen/README.txt
 |  Style URL: http://192.168.222.166/wp-content/themes/twentyseventeen/style.css
 |  Theme Name: Twenty Seventeen
 |  Theme URI: https://wordpress.org/themes/twentyseventeen/
 |  Description: Twenty Seventeen brings your site to life with header video and immersive featured images. With a...
 |  Author: the WordPress team
 |  Author URI: https://wordpress.org/

[+] Enumerating plugins from passive detection ...
[+] No plugins found

[+] Finished: Wed Jul  5 21:56:08 2017
[+] Requests Done: 68
[+] Memory used: 17.34 MB
[+] Elapsed time: 00:00:01
```



# References
1. [Category:OWASP DirBuster Project](https://www.owasp.org/index.php/Category:OWASP_DirBuster_Project)
2. [The Web Robots Pages](http://www.robotstxt.org/robotstxt.html)
3. [Nikto 2 | Cirt.net](https://cirt.net/nikto2)
4. [GitHub - wpscanteam/wpscan: WPScan is a black box WordPress vulnerability scanner.](https://github.com/wpscanteam/wpscan)
5. [WordPress - Wikipedia](https://en.wikipedia.org/wiki/WordPress)
6. [Usage Statistics and Market Share of Content Management Systems for Websites, July 2017](https://w3techs.com/technologies/overview/content_management/all)
7. [Launch a WordPress Bruteforce Attack with WPScan](https://www.wpwhitesecurity.com/wordpress-tips-webmasters/strong-wordpress-passwords-wpscan/)
