## Write up

I started with the nmap scan to see the open ports.

```
nmap -sV -sC -oA nmap 10.10.10.8
```

Generated 3 nmap output files and opened the nmap.nmap file.

This is the content of the nmap.nmap file

`# Nmap 7.50 scan initiated Mon Jul 10 21:13:26 2017 as: nmap -sV -sC -oA nmap 10.10.10.8`

`Nmap scan report for 10.10.10.8`

`Host is up (0.55s latency).`

`Not shown: 999 filtered ports`

`PORT   STATE SERVICE VERSION`

`80/tcp open  http    HttpFileServer httpd 2.3`

`|_http-server-header: HFS 2.3`

`|_http-title: HFS /`

`Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows`

`Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .`

`# Nmap done at Mon Jul 10 21:14:33 2017 -- 1 IP address (1 host up) scanned in 67.96 seconds`

The port 80 is open and it uses HttpFileServer httpd 2.3. I opened the msfconsole \(metasploit\) to search and see the available exploits for the current version of HttpFileServer \(HFS\). I used the search command as shown below.

```
msf > search hfs
```

And it shows the matching modules.

```
Matching Modules
================

   Name                                        Disclosure Date  Rank       Description
   ----                                        ---------------  ----       -----------
   exploit/multi/http/git_client_command_exec  2014-12-18       excellent  Malicious Git and Mercurial HTTP Server For CVE-2014-9390
   exploit/windows/http/rejetto_hfs_exec       2014-09-11       excellent  Rejetto HttpFileServer Remote Command Execution
```

Here, we can see already the available exploit for the HttpFileServer \(HFS\).

I used the `exploit/windows/http/rejetto_hfs_exec`as the exploit.

```
msf > use exploit/windows/http/rejetto_hfs_exec
```





