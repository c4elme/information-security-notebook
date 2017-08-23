# Notes and Techniques

## Reconnaissance

* search for available information about the target
* for the meantime, use passive reconnaissance for finding information about the target \(google-fu, company profile, social media, name servers, etc.\)
* use active reconnaissance but be careful in dealing with firewalls, IDS, and IPS
* list all the available information that can be used to attack the target \(for example, information that can be used to social engineer the target\)
* use tools like Nmap to scan the target for the available services on his/her local machine
* Some tools for reconnaissance:
  * nmap
  * maltego

## Enumeration

* check for the versions of the available services that are present on the target's local machine
* you can use automated scripts to automate the enumeration process
* look out for the low hanging fruits, for example, there may be a hidden file, weak passwords, default config files and others
* Some tools for enumerating the target:
  * Linux Privilege Escalation Enumeration Scripts
    * unix-privesc-check - http://pentestmonkey.net/tools/audit/unix-privesc-check
    * linuxprivchecker.py - https://gist.github.com/sh1n0b1/e2e1a5f63fbec3706123
    * linenum - https://www.rebootuser.com/?p=1758
    * linux-local-enumeration-script.sh - https://highon.coffee/blog/linux-local-enumeration-script/

## Exploitation

* proper enumeration can lead to easier exploitation
* you can use public exploits to attack the vulnerable services that are available on the target's local machine
* public exploits may not work out of the box so you need to analyze how the exploit works by tracing the source code of the exploit
* modify the source code of the exploit if you need to
* in compiling public exploits locally, make sure that it matches the kernel version of the local machine to the target machine

## Post Exploitation

* if you have gained access to the system, you may install a backdoor in the case of the user reboots the target machine
* since you only have an initial access to the system \(low privileged access\), enumerate for the available programs, weak credentials, default passwords, and others that may be used to escalate your privileges
* 
## Covering Tracks

* remove the backdoors and other files that you used to gain access to the target
* delete or modify the log files



