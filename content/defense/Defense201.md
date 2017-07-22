---
title: "Defense 201"
date: 2017-06-23T04:46:35Z
---

# Welcome to Defense 201

Congratulations!  You finished Defense 101 and are moving up in the world.  The last scenario consisted of challenges requiring basic log analysis skills and basic threat intelligence research to accomplish.  This scenario will build on what we learned in Defense 101 and extend to other areas like file triage analysis and some WireShark techniques that are often required.  Below we will run through a few examples and resources that will help you complete this scenario.

## Wireshark File Extraction from Network Traffic

Be sure you have downloaded [Wireshark](https://www.wireshark.org/).  You may also want to explore other tools like NetworkMiner, but for the purposes of this CTF, we'll be using Wireshark.

Extracting files from HTTP traffic is surprisingly easy with Wireshark.  The video below will demonstrate how to extract the file using Wireshark's built-in file object parsing as well as how to manually export the raw bytes to a local file.  Some protocols, like FTP will require the later method to extract files from network streams.

[![Wireshark Extracting Files](https://i.ytimg.com/vi/BEd08qDYgGQ/hqdefault.jpg)](https://youtu.be/BEd08qDYgGQ)

## Remnux - Viper

In order to start giving us a taste of malware file triage analysis, we will learn a few basic concepts and walk through a basic example with the web interface of [Viper](http://viper.li/).

### First, let's get Viper up and running

Open a terminal.  Create a new directory for yourself where you will work with viper and change directories into it.  Then simply run the viper docker container.

```
mkdir viper
cd viper
docker run --rm -p 127.0.0.1:9090:9090 remnux/viper
```

Finally, open a web browser and navigate to http://127.0.0.1:9090 and you should see a page like the following.

![Viper](/defense/viper_started.png)

### Loading a Windows Executable in Viper

In this training, we will only be working with non-malware samples to keep things easy.  We don't want to frustrate learners by having their malware samples used for training wiped from their machine.  Worse yet, if you are unwisely using a company asset for this training, you could get contained by your response team because of the malware that's accidentally exposed to your corporate asset.  For these reason's, we are avoiding actual malware for these introductory training sessions.

Go ahead and download the [ProcDump](https://technet.microsoft.com/en-us/sysinternals/dd996900.aspx) tool from Microsoft.  This should be a single zip file.  After unzipping the archive, there will be a file procdump.exe.

Returning to your Viper instance, under "Upload Sample", click "Choose file" and click the Upload button on the far right.  Make sure you pick procdump.exe, not procdump64.exe if you are going to follow along.

![Viper](/defense/viper_upload_file.png)

The file should then appear at the bottom of the page in the Project area.  Click on the file name of the uploaded file area "procexp.exe" and a new page will be loaded, giving you additional file information.

![Viper](/defense/viper_file_summary.png)

Notice you get several different hash computations.  These are unique values representing the content of the executable.  If anything in the procexp.exe changes, the hash values will all change.  This allows analysts to communicate with each other about a file and know whether or not they are talking about the same file.

### Basic Information from an Executable
Click on the Modules link.  Notice there are many modules and within each module, there are additional commands that can be run.  Select the "Exif - Extract MetaData" module and click the "Run" button on the far right.

![Viper](/defense/viper_module_selection.png)

Notice it found the CompanyName and File Description related to Sysinternals within the executable.  The version number and copyright information is present.  We get a timestamp for the executable as well as the mimetype for the file.

Let's run the "PE - Parse PE32 files" Module and select the "PEID" command and click the "Run" button.  PE ID is a tool that provides information about what language an executable was written in and whether or not the file appears to have been packed.  Packing executables is a practice that commercial software does as well as malware in an effort to make it more difficult to reverse engineer.

Now run the "Digital Certificates" command.  Notice it can generate the hash of the certificate that was presumably used to sign the executable.

![Viper](/defense/viper_digital_certificate.png)

Other areas you may want to explore include the Sections, Imports, and Exports of a binary.  The sections and the entropy of each section can be used to help determine if a file is packed.  The imports and exports can provide information about what functionality a file might have.  Imports and exports of an executable are so important that their values themselves can be used to identify families of malware.  For more information, read about [Tracking Malware with Import Hashing](https://www.fireeye.com/blog/threat-research/2014/01/tracking-malware-import-hashing.html).

There is a module to look for shellcode, usually you're looking for this embedded in a file type (e.g. pdf, office document etc).  It is also known to have a lot of false positives.

![Viper](/defense/viper_shellcode.png)

Analyzing the strings of an executable is also a must-do step in basic file analysis.  If the malware is packed, there is typically not a lot of information that can be recovered without first unpacking the malware, which is a task beyond the scope of this training session.

However, if the file is not packed, it can reveal the structure of HTTP requests, configuration of malware, as well as IP addresses and domains the malware uses.

If you run the "Strings - Extract strings" function within Viper and search down for "http:", you'll notice several Microsoft domains and subdomains within this file as well as function names that the executable uses that can provide some indication of what the executable does if it were to be executed.  Occasionally an attacker won't realize that the directory path for their development environment is present in the executable they generate and can allow for detection and attribution to a particular adversary.

There are a lot of tools here and we're not attempting to cover all malware analysis in this tutorial, rather this was intended to be an introduction to some of the tools available.  


<a href="http://learn.greyhatctf.com/defense/defense101/"><button type="button" class="btn btn-Primary btn-arrow-left">Prev Article</button></a>
