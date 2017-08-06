Nmap scan

```
# Nmap 7.40 scan initiated Fri Jul 21 04:41:25 2017 as: nmap -sV -sC -oA nmap 10.10.10.14
Nmap scan report for 10.10.10.14
Host is up (0.33s latency).
Not shown: 999 filtered ports
PORT   STATE SERVICE VERSION
80/tcp open  http    Microsoft IIS httpd 6.0
| http-methods: 
|_  Potentially risky methods: TRACE COPY PROPFIND SEARCH LOCK UNLOCK DELETE PUT MOVE MKCOL PROPPATCH
|_http-server-header: Microsoft-IIS/6.0
|_http-title: Under Construction
| http-webdav-scan: 
|   Public Options: OPTIONS, TRACE, GET, HEAD, DELETE, PUT, POST, COPY, MOVE, MKCOL, PROPFIND, PROPPATCH, LOCK, UNLOCK, SEARCH
|   WebDAV type: Unkown
|   Server Date: Thu, 20 Jul 2017 20:42:02 GMT
|   Server Type: Microsoft-IIS/6.0
|_  Allowed Methods: OPTIONS, TRACE, GET, HEAD, COPY, PROPFIND, SEARCH, LOCK, UNLOCK
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
# Nmap done at Fri Jul 21 04:42:16 2017 -- 1 IP address (1 host up) scanned in 50.31 seconds
```

I searched for some exploits in webdav and found one.

```
exploit/windows/iis/iis_webdav_scstoragepathfromurl       2017-03-26       manual      Microsoft IIS WebDav ScStoragePathFromUrl Overflow
```

That exploit can be used to have a meterpreter session.

After I got a session it turns out that the machine privileges has the Token privs something by running the **getprivs** command. So I searched for the token kidnapping exploit and it was available in exploit-db site: [https://www.exploit-db.com/exploits/6705/](https://www.exploit-db.com/exploits/6705/)

I uploaded the exe file \(churrasco.exe\) and executed it on the command prompt of the vulnerable machine and it turns out that I had an Administrator privilege on the machine.

```
> churrasco.exe "cmd.exe"
```

The command means  that the churrasco.exe will run the given command which is the "cmd.exe".



# Can be used on HTB/Granny



