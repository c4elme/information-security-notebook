msf auxiliary\(smb\_enum\_gpp\) &gt; use auxiliary/scanner/smb/smb\_ms17\_010

msf auxiliary\(smb\_ms17\_010\) &gt; show options



Module options \(auxiliary/scanner/smb/smb\_ms17\_010\):



   Name       Current Setting  Required  Description

   ----       ---------------  --------  -----------

   RHOSTS                      yes       The target address range or CIDR identifier

   RPORT      445              yes       The SMB service port \(TCP\)

   SMBDomain  .                no        The Windows domain to use for authentication

   SMBPass                     no        The password for the specified username

   SMBUser                     no        The username to authenticate as

   THREADS    1                yes       The number of concurrent threads



msf auxiliary\(smb\_ms17\_010\) &gt; set RHOSTS 10.10.10.4

RHOSTS =&gt; 10.10.10.4

msf auxiliary\(smb\_ms17\_010\) &gt; run



\[+\] 10.10.10.4:445        - Host is likely VULNERABLE to MS17-010!  \(Windows 5.1\)

\[\*\] Scanned 1 of 1 hosts \(100% complete\)

\[\*\] Auxiliary module execution completed



