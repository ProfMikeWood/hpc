# Prerequisites

If you're interested in using Spartan, there's a few things you'll need to have in hand to get started.

## SJSU Credentials
The primary prerequisite for accessing Spartan is a set of credentials (email address and ID number) for San José State University. These are automatically provided to SJSU faculty, affiliates, and students. This includes students in the Moss Landing Marine Labs graduate program that are enrolled through CSU Monterey Bay.

## Access to the SJSU VPN
Another prerequisite for accessing Spartan is access to the SJSU VPN. Spartan is behind the VPN for security purposes. To find out more information about the SJSU VPN, see the page here: https://www.sjsu.edu/it/services/network/vpn.php

As an SJSU faculty member or student with SJSU credentials, you should have access to the VPN. However, there have been some circumstances when the credentials have not been automatically listed on the roster of approved users. If you are having issues with the VPN, submit an IT Ticket on the Spartan IT help desk here: https://isupport.sjsu.edu/Helpdesk/Dashboard

## Spartan Credentials
Aften ensuring your SJSU credentials are active and that you have access to the SJSU VPN, next you will need credentials and an account on Spartan. All Spartan users must either be a faculty member at SJSU or sponsored by a faculty member at SJSU. In other words, if you are student, you will need to ask an SJSU faculty member to request credentials on your behalf.

```{note}
CSUMB students in the MLML graduate program should reach out to the MLML/SJSU faculty member on their thesis committee for assistance. 
```

### For Faculty: Requesting Access to Spartan
If you are a faculty member interested in requesting access to Spartan for you or your students, put in a **HPC New User Request** on the page here: https://isupport.sjsu.edu/cos/Dashboard

```{important}
If you are a faculty member unfamiliar with running jobs, please reach out to me (Mike Wood, mike.wood@sjsu.edu) to let me know. I am happy to help students/faculty (with reasonable notice) because Spartan is a great resource - but it is also a tad fragile and benefits from a little TLC.
```

## A Command Line Terminal

Spartan, like all computing clusters, is typically accessed through a Unix command line terminal. The terminal you use will depend on your operating system.

### MacOS

If you are on a Mac, you call just use the typical terminal provided by the terminal app (just search for Terminal in your App menu).

### Windows 

On Windows, there are a few different options for accessing Unix-type shells. I recommend installing the Windows Subsystem for Linux (WSL). You can install this by searching for the Powershell and running the following command:

```
wsl --install
```

Note that you can install different Linux distributions but the default will be Ubuntu (recommended). After the installation has completed, you will be able to open your Linux distribution from the start menu (e.g. search for Ubuntu if you used the default wsl installation). Note that you will need to make a new “user” for Ubuntu with a password - this is separate from your windows user name and password. Its recommended that you create your username without spaces to avoid issues with your path.

```{tip}
If you are unfamiliar with command line tools, I recommend that you build up some basic skills using available online tutorials. I recommend the Software Carpentry Shell Tutorial available here: https://swcarpentry.github.io/shell-novice/. The first three parts of that tutorial, at least, will help you become familiar with the command line.
```


Once you've got all of the prerequisites above, you'll be set to access Spartan. Click on the next page to see how to access and navigate the machine.