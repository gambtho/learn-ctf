---
title: "Threat Detection Introduction"
date: 2017-06-26T04:46:35Z
---

# Purpose

The purpose of this training material is to provide enough basics to get a good start on each of the challenges.  At the same time, you will be acquiring and practicing the necessary skills to be an effective cyber threat detection analyst.

## Guiding Principles

Whether we like it or not, we must accept that our systems and networks will be compromised and we need to assume that is already the case.

 - *Assume Compromise:* During this exercise and in your organization, you must assume networks and systems are already compromised
 - *Attackers are People:* Attackers are people and have habits, preferred tools, and reuse attack patterns.  These are referred to as Tactics, Techniques, and Procedures (TTPs).
 - *Remove Attacker Options:* Adversary TTPs are a weakness we can exploit to frustrate them.  By reliably detecting these TTPs, we remove them from our attacker's available options, kick them out of our systems and we win.
 - *Stop Them Before They Win:* Adversaries win if they can successfully complete each of the necessary steps in their particular "kill chain".  A Cyber Kill Chain is the succession of actions the attacker must complete in order to accomplish their objective.  Most kill chains have many steps necessary to complete, giving defenders some precious time to detect and respond to their advances.

## Defender Tools Overview

Many of the exercises will leverage Bro Network Security Monitor (NSM) logs and packet capture files.  NSM logs can be easily imported into an analytics platform like the combination of Elasticsearch, Logstash, and Kibana commonly called an ELK stack (or Elastic Stack).

### Bro Network Security Monitor (NSM)

[Bro NSM](https://www.bro.org/) provides network metadata.  This metadata provides insight about what happened on a network and it is up to the user of the information to derive their own meaning.  Your job during these exercises will typically be to analyze the logs and determine the details of definite or likely malicious activity and discern it from benign activity.  This is often a surprisingly difficult task and requires hands-on experience, which is why this training is hands-on.

### Elasticsearch, Logstash, and Kibana

This collection of technologies brings adds a quick log analysis web application with powerful search and visualization capabilities.  We'll be spending the majority of our time using this collection of technologies to explore the Bro NSM logs.  For those interested, you are encouraged to visit the official website for the [Elastic Stack](https://www.elastic.co/webinars/introduction-elk-stack).

### Wireshark

Although there are several packet analysis tools, both graphical and command line, Wireshark is a standard tool that anyone in the threat detection and response field should be comfortable with.  We strongly recommend just installing this tool on your host or VM directly, rather than looking at dockerized solutions.  The tool can be downloaded from the [Wireshark Website](https://www.wireshark.org/), but it is also available in most Operating System repositories.

### REMNUX

There are various tools and methods for performing file triage analysis.  A basic set of tools will be leveraged, but you are certainly not limited to the set of tools documented in this material.

We'll be using [Remnux Docker Images](https://hub.docker.com/r/remnux/) for our analysis.  The documentation can be found [here](https://remnux.org/docs/containers/malware-analysis/), but we'll walk through what is needed together.