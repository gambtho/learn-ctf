---
title: "The Cyber Attack Lifecycle"
date: 2017-06-27T02:03:27Z
draft: true
---
# Introduction
Cyber attackers have an operating cycle that is common across many attacks. This cycle can be called the attack lifecycle. There are various models to explain how the lifecycle works by many different organizations including Lockheed Martin, Palo Alto Networks, and Mandiant (see References section for links). If you read each variation of the lifecycle you will find that you can summarize the lifecycle into reconnaissance, exploitation, privilege escalation, and actions on objective phases. 

The purpose of this article is to give you a mental model of how real attackers operate. By understanding the attack lifecycle you will be able to incorporate the same cycle into penetration testing. The main difference between real attacks and penetration testing is the enforcement of strict limits on what you can exploit and what you can do on your objective. In the following sections, I will summarize each stage of the attack lifecycle.

In the following sections, I use the the term attacker in the singular form but often attackers operate in teams. I will still use the singular form even when referring to teams of attackers.

## Reconnaissance
In the reconnaissance phase, attackers perform passive and active reconnaissance. The ultimate goal of reconnaissance to identify weaknesses in the target networks to exploit. Good reconnaissance increases the chances that the next phase of the attack lifecycle will be successful.

### Passive reconnaissance
Passive reconnaissance refers to reconnaissance in a such a way that the target network is not touched by packets from the attacker. This includes the following:
* Whois lookups
* Search engine queries
* Social media profiles
* SEC filings
* Public legal documents

### Active Reconnaissance
Active reconnaissance involves touching the target network with packets from the attacker, and this includes packets coming through proxy channels. Active reconnaissance includes the following:
* Browsing target owned websites (e.g. corporate websites)
* Scanning of target networks
* Enumerating systems

## Exploitation

## Privilege Escalation

## Actions on Objective


# References
1. [Breaking the Cyber Attack Lifecycle by Palo Alto Networks](https://data.bloomberglp.com/bgov/sites/12/2015/12/Underwriter-Content-Palo-Alto-Breaking-the-Cyber-Attack-Lifecycle.pdf)

2. [The Cyber Exploitation Life Cycle by InfoSec Institute](http://resources.infosecinstitute.com/the-cyber-exploitation-life-cycle/)

3. [Cyber Attack Lifecycle by Law Enforcement Cyber Center](http://www.iacpcybercenter.org/resource-center/what-is-cyber-crime/cyber-attack-lifecycle/)

4. [The Cyber Kill Chain® by Lockheed Martin](http://www.lockheedmartin.com/us/what-we-do/aerospace-defense/cyber/cyber-kill-chain.html)

