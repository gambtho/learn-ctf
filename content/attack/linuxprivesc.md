---
title: "Linux Privilege Escalation"
date: 2017-07-20T21:08:59Z
draft: true
---

# Introduction
So you've got a shell on your target but you're on with a limited user account. You need root privileges to get finish exploiting your target. The question then is, "How do I get root?". This article will give you some techniques to escalate to root on Linux systems.

# Enumerate the system
The first thing you want to do is the gather information about the Linux host you are on.

Figure out who you are with these two commands.
```
whoami
id
```

Try figuring out what OS version with the following commands
```
uname -a
cat /etc/os-release
cat /proc/version
```

Once you enumerate the system do a search for vulnerabilities for the OS and version numbers. Check CVEs, Exploit Database, Google, GitHub, etc. If you find something that matches take time to examine the exploit and see if you can use it on the system you're attacking.

# sudo
If you know the limited user password you can try to see if you can execute ```sudo``` commands. ```sudo``` is a Linux command that allows you execute commands as usually as root. If you can execute ```sudo``` as your limited user, you may be done if they gave the limited user all commands in the /etc/sudoers file.

# SUID
SUID is short for set user ID upon execution. They are set with special file permission flags. Normally when a user executes a program, the program executes with the same permissions as the user. However, if the SUID is set, then the program will run with the permissions of the owner of the file not the user which launched it.

To find all files with the sticky bit set use the following command.
```
find / -perm -4000 2>/dev/null
```

If you can find a program with the sticky bit set that can write to files or execute commands you can escalate privileges with that program.

# References
1. [Basic Linux Privilege Escalation](https://blog.g0tmi1k.com/2011/08/basic-linux-privilege-escalation/)
2. [What You Should Know About the sudo Command](https://www.lifewire.com/what-to-know-sudo-command-3576779)
3. [What is SUID and how to set SUID in Linux/Unix? - The Linux Juggernaut](http://www.linuxnix.com/suid-set-suid-linuxunix/)