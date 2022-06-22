# WildIris HPC Tutorial


![](images/WildIris.png)


## Under active development!!!

This tutorial will walk through the basics of the WildIris high-performance computing (HPC) cluster that is hosted at the University of Wyoming (UW). This cluster is specifically implemented to support users outside of UW and does not require UW credentials/email for access.

If you are looking at this tutorial, then I'm assuming that you already have login credentials that were provided by UW's Advanced Research Computing Center (ARCC -- my sincere apologies for all the acronyms, I hate 'em, too). 


## Table of contents:




## Logging in

Logging into WildIris follows the same general procedure as logging into most remote servers. If you are on a Mac or running a Linux operating system, then you can log in directly from the terminal. If you are on a Windows machine, you will need to install an ssh client to allow you to log into and communicate with WildIris, such as [MobaXterm ](https://mobaxterm.mobatek.net/download.html) or [PuTTY](https://www.putty.org/).


Detailed instructions for logging into WildIris are described on ARCC's site [here](https://arccwiki.atlassian.net/wiki/spaces/DOCUMENTAT/pages/1566048281/Connecting+to+WildIris). We'll assume that you've completed your first login. At this point, on a Mac or Linux, you can open a terminal window, type 

`ssh <username>@wildiris.arcc.uwyo.edu`

(where <username> should be replaced by your username on the system)

Then when prompted for a password, enter your password. You will then be asked for a second password: enter the code provided by the FreeOTP app.

This will work basically the same in MobaXterm or PuTTY, but you will put `<username>@wildiris.arcc.uwyo.edu` into the hostname/session window instead of entering it on the command line.

If you've correctly entered your password and FreeOTP code, you should now be logged into WildIris.





- Cyberduck is hella useful


- WildIris is a Linux system. etc, basic navigation and setup, intro bash


- Basic architecture of WildIris: number of nodes and cores
	- worker vs. login node - DON'T do stuff on login node
	- Salloc session
	- jobs
	



this is a good template guide from Teton: https://microcollaborative.atlassian.net/wiki/spaces/DSC/pages/102563845/Teton+beginner+s+guide

