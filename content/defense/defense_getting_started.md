---
title: "Defense Scenario: Getting Started"
date: 2017-06-25T04:46:35Z
---

# First Scenario: Banking Trojan Infection

In the first set of challenges, we will be analyzing Bro Network Security Monitoring (NSM) logs consisting of both benign and malicious traffic.  If you aren't already familiar with [Bro NSM logs](https://www.bro.org/sphinx/), you soon will be.  For this set of challenges, you are provided with a set of tools, mostly docker-compose and docker files that launch analysis environments and give you access to the forensic artifacts to base your analysis on.


## Pre-requisites

These challenges were built and tested on Ubuntu Desktop.  The exercises should work without issue on Linux and Mac machines.  If they do not work well on Windows, it is recommended to use Virtual box or other virtualization software and an Ubuntu Desktop VM.

The host you will be running the exercises on will require Docker and Docker Compose to both be installed and confirmed to be working.  The install instructions for both are found here:

* [Docker Install](https://www.docker.com/community-edition)
* [Docker Compose Install](https://docs.docker.com/compose/install/)


## Setup

After installing and confirming the pre-requisites work as expected, you need to get and extract the exercises repository:

* Download the git repo by either navigating to the github repo site [GreyHatCTF_ELK](https://github.com/egaus/greyhatctf_elk)  via a web browser and downloading and unzipping the repository using the green "clone or download" button
OR
* Clone the repository with git

> `git clone https://github.com/egaus/greyhatctf_elk.git`


After cloning the repository and extracting the contents, if you are in the top level directory that contains the docker-compose.yml file, you can then start the environment with Docker compose with the following command:

> `docker-compose up`



