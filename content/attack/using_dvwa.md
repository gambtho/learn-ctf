---
title: "Using DVWA"
date: 2017-07-28T15:28:00Z
draft: true
---

# Introduction
The Damn Vulnerable Web Application (DVWA) is purposely vulnerable web application that is hosted in our lab. The application is designed to assist training attacking various web application vulnerabilities. Most of the common web vulnerabilities are tested including cross site scripting, SQL injection, local file inclusion, remote file inclusion, directory traversal, command injection, and weak credentials.

# Accessing DVWA
Ensure that you can access the lab environment through the VPN tunnel. See [Accessing the Lab](http://learn.greyhatctf.com/attack/accessinglab/) for more details on VPN connection configurations.

Once you have your VPN connection up, open a web browser and go to http://<DVWA IP>/dvwa/. This will only work with an active VPN connection.

You'll see a web page with a login form. 
![DVWA login](/attack/dvwa_login.png)
Use admin:password to login.

# Using DVWA
Once you are logged in you'll see a welcome page. Read through the welcome page and click the DVWA Security link on the navigation bar on the left.
![DVWA Welcome](/attack/dvwa_welcome.png)

In the security page, I recommend that you put the security setting on Low and start training from there. To do this select Low from the drop down menu and click submit. You can raise levels as needed as you advance your security training.
![DVWA Security](/attack/dvwa_security.png)

Once you've done that you can navigate to any of the challenges and start attacking.
![DVWA Challenges](/attack/dvwa_challenges.png)

Inside each of the challenge pages you'll find a small web app that allows you to test your web application penetration testing skills. You'll also find links to more information resources to help you.

If you mess anything up in the web server you can reset it by going Setup / Reset DB page and clicking the Create / Reset Database button at the bottom of the screen.
![DVWA Database Setup](/attack/dvwa_db_setup.png)

That's all there is to it. Don't be afraid to try new things and don't worry about messing up the web application. It's designed to be messed with and attacked.

Happy hacking!

# References
[DVWA - Damn Vulnerable Web Application](http://www.dvwa.co.uk/)