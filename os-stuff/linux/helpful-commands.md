## List of Useful Commands in Linux [here](http://resources.infosecinstitute.com/useful-linux-commands/#gref) and [here](http://linuxcommand.org)

## Command Substitution

Command substitution allows us to use the output of a command as an expansion:

`[me@linuxbox me]$echo $(ls)  
Desktop Documents ls-output.txt Music Pictures Public Templates Videos`

`[me@linuxbox me]$ls -l $(which cp)  
-rwxr-xr-x 1 root root 71516 2007-12-05 08:58 /bin/cp`

Source: http://linuxcommand.org/lc3\_lts0080.php



