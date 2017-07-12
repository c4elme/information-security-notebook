## List of ALL Useful Commands in Linux [here](http://resources.infosecinstitute.com/useful-linux-commands/#gref) and [here](http://linuxcommand.org)

## 

## Command Substitution

Command substitution allows us to use the output of a command as an expansion:

`[me@linuxbox me]$echo $(ls)          
Desktop Documents ls-output.txt Music Pictures Public Templates Videos`

`[me@linuxbox me]$ls -l $(which cp)          
-rwxr-xr-x 1 root root 71516 2007-12-05 08:58 /bin/cp`

## chmod

The chmod command is used to change the permissions of a file or directory. To use it, you specify the desired permission settings and the file or files that you wish to modify. There are two ways to specify the permissions. In this lesson we will focus on one of these, called the octal notation method.

It is easy to think of the permission settings as a series of bits \(which is how the computer thinks about them\). Here's how it works:

```
rwx rwx rwx = 111 111 111
rw- rw- rw- = 110 110 110
rwx --- --- = 111 000 000

and so on...

rwx = 111 in binary = 7
rw- = 110 in binary = 6
r-x = 101 in binary = 5
r-- = 100 in binary = 4
```

## Changing File Ownership

You can change the owner of a file by using the chown command. Here's an example: Suppose I wanted to change the owner ofsome\_filefrom "me" to "you". I could:

`[me@linuxbox me]$su    
Password:    
[root@linuxbox me]#chown you some_file    
[root@linuxbox me]#exit    
[me@linuxbox me]$`

Notice that in order to change the owner of a file, you must be the superuser. To do this, our example employed the su command, then we executed chown, and finally we typed exit to return to our previous session.

chownworks the same way on directories as it does on files.

## Changing Group Ownership

The group ownership of a file or directory may be changed with chgrp. This command is used like this:

`[me@linuxbox me]$ chgrp new_group some_file`

In the example above, we changed the group ownership ofsome\_filefrom its previous group to "new\_group". You must be the owner of the file or directory to perform a chgrp.

Source: [http://linuxcommand.org/lc3\_lts0080.php](http://linuxcommand.org/lc3_lts0080.php)

