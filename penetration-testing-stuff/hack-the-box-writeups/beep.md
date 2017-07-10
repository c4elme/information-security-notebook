**Enumeration**

**NMAP scan**

`root@kali:/home/kai# nmap -sS 10.10.10.7`

`Starting Nmap 7.50 (`[`https://nmap.org`](https://nmap.org)`) at 2017-07-08 22:17 +08`

`Nmap scan report for 10.10.10.7`

`Host is up (0.40s latency).`

`Not shown: 988 closed ports`

`PORT      STATE SERVICE`

`22/tcp    open  ssh`

`25/tcp    open  smtp`

`80/tcp    open  http`

`110/tcp   open  pop3`

`111/tcp   open  rpcbind`

`143/tcp   open  imap`

`443/tcp   open  https`

`993/tcp   open  imaps`

`995/tcp   open  pop3s`

`3306/tcp  open  mysql`

`4445/tcp  open  upnotifyp`

`10000/tcp open  snet-sensor-mgmt`

`Nmap done: 1 IP address (1 host up) scanned in 141.70 seconds`

**NC Listening to port 25 \(smtp\)**

`kai@kali:~$ nc 10.10.10.7 25`

`220 beep.localdomain ESMTP Postfix`

`VRFY root`

`252 2.0.0 root`

`msf auxiliary(smb_version) > use auxiliary/scanner/smtp/smtp_enum`

`msf auxiliary(smtp_enum) > set RHOSTS 10.10.10.7`

`RHOSTS => 10.10.10.7`

`msf auxiliary(smtp_enum) > exploit`

`[*] 10.10.10.7:25         - 10.10.10.7:25 Banner: 220 beep.localdomain ESMTP Postfix`

`[+] 10.10.10.7:25         - 10.10.10.7:25 Users found: , adm, bin, daemon, fax, ftp, games, gdm, gopher, haldaemon, halt, lp, mail, news, nobody, operator, postgres, postmaster, sshd, sync, uucp, webmaster, www`

`[*] Scanned 1 of 1 hosts (100% complete)`

`[*] Auxiliary module execution completed`

`msf auxiliary(smtp_enum) >`

Users Found after the SMTP\_ENUM

`Users found: , adm, bin, daemon, fax, ftp, games, gdm, gopher, haldaemon, halt, lp, mail, news, nobody, operator, postgres, postmaster, sshd, sync, uucp, webmaster, www`

