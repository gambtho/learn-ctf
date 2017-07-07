---
title: "We Love Shells"
date: 2017-07-06T03:00:20Z
draft: true
---

# Introduction
A shell is a user interface that gives interactive access to a host. Typically shells that attackers user will be on a command line interface (CLI).

On Linux the most common shell is Bash and on Windows the most common shell is cmd.exe and PowerShell. The shells on both Linux and Windows systems allow a user to interact with the system in almost any way he wants as long he has the appropriate permissions.

Learning how to use Bash or cmd.exe or PowerShell is outside of the scope of this lessons here. You can find entire books written on the subject of learning how to use those shells. I'll refer you to the references section for more resources on learning shell interfaces.

Shellcode refers to a piece of code that used as part of payload from an attacker to a victim. Once the shellcode is on the victim machine it can then provide interactive shell capabilities to the attacker.

# Types of Shells
There are two primary types of shellcode used by attackers. These are the bind shell and reverse shell which are explained in further detail below.

## Bind Shell
A bind shell is the simpler of the two types of shellcode used by attackers but is less likely to evade firewalls. The bind shell is created when the attacker initiates a connection to the host (usually over TCP/IP) and sets up a remote shell.

### Steps

1. Victim binds a shell to a port and listens on that port for incoming connections
2. Attacker sends a connection request listening port on the victim machine.
3. Attacker get an interactive shell (e.g. bash or cmd.exe)

## Reverse Shell
A reverse shell is usually preferred method for attackers to get an interactive shell on their victim. A reverse shell creates an outbound connection from the victim to the attacker. Since most firewalls allow outbound connections from hosts inside the network the attacker can usually evade firewalls which may prevent him from getting a bind shell!

### Steps

1. Attacker sets up a listener on a port on a machine he controls
2. Victim hosts sends connection request to the attacker on listening port and sends a shell upon connecting
3. Attacker gets an interactive shell (e.g. bash or cmd.exe)

# References

1. [Shell (computing) - Wikipedia](https://en.wikipedia.org/wiki/Shell_(computing))
2. [Using Windows PowerShell](https://msdn.microsoft.com/powershell/scripting/getting-started/fundamental/using-windows-powershell)
3. [LinuxCommand.org: Learn the Linux command line. Write shell scripts.](http://linuxcommand.org/index.php)
4. [Shellcode - Wikipedia](https://en.wikipedia.org/wiki/Shellcode)
