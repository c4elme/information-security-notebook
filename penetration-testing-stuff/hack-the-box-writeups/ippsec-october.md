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
  * 



