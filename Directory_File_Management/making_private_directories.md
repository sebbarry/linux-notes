# This file overviews what we need to do to set and configure set GID directories for collaboration.

> These can be shared by users of a specific group.


## 1. Lets first start by making a group that will have the rights to the directory.
command: ```groupadd -g <id> <new group name>```


## 2. Make a directory to share: 
command: ```mkdir /home/<name of shared dir>```


## 3. CD into the new directory

## 4. Change the ownership of the directory: 
command: ```chown nobody:<new group name> <name of directory to share>```


## 5. Modify the default modifications for the group:
command: ```chmod g+sw /home/<name of dir>```
<pre> drwxrwsr-x. 2 nobody    group01     6 Oct 26 17:05 shared_dir </pre>


## 6. Finally, remove permissions from other users:
command: ```chmod o-rwx /home/<name of directory to share>```





