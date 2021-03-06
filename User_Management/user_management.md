# User Accounts and Managemenent Overview. 

All users accounts have: 
1. username
2. uid (user id)
3. default group
4. comments
5. shell. 
6. home directory location

> All this information is stored in the etc/passwd file

## etc/passwd file
It contains: 
```
...
username:password:UID:GID:comments:home_dir:shell

```
*The first listing in the etc/passwd file is the root account. 

- We can read passwords from the /etc/shadow file.
- The root account is always UID 0
- We can assign users to certain groups to make files.
- A user is always placed into the home directory.


## etc/shadow file 
contains a list of passwords 
*refer to an online resource for field partitions



## Creating a user 

```
useradd [options] username
```

[options]:
```
 -c ('comment')
-m (create the home directory automatically)
-s <provide the path to the user's defualt shell.>
-r to create a system account (used to application and system accounts (think db account))
-d set the directory of the user manually (commonly when making a system account)
-g <default group name>
-G non default project.
```

ex: 
```
useradd -c "sebastian barry" -m -s /bin/bash sebastian (to create a new user)
passwd sebastian (to enter a password)
```

**Note**
> Not every account is meant to be used by a person
> Some accounts are created to run system processes, database processes, and other application processes.

*To create a system or application account make sure to set the shell ( ```-s``` ) as:*
- ```/usr/sbin/nologin``` 

 **Or** 

- ``` useradd -r -s /usr/sbin/nologin <username> ``` 

This is because we dont want the user to be able to login to the system using taht account.


### Delete an account 
```
userdel -r username
```

### Change an account 
```
usermod 
```

### Switching accounts 
```
su (switches to sudo account)
su <username> (switches to particular account)
```



## Managing Group Details 

group details are found in the ```/etc/group``` file
```
groupname:password:GID:account1, ...accountn
```

show groups with: ```groups``` command 
```
groups <groupname>
```

Show a user's group with: groups <user>

1. create a group: 
groupadd <name> 
2. delete a group: 
groupdel <name>
3. modify a group: 
groupmod [options] <namegroup>
-g <value> : change the group id  
-n <group> : rename the group 


## Exampled: Create groups: 
```
#make 3 groups
groupadd writers 
groupadd tv
groupadd movie
#show the last three lines of the /etc/group file
tail -3 /etc/group
#add a user to a particular group
useradd -c "User A" -g writers -G tv -m -s /bin/bash usr_a
#give the user a password
passwd usr_a 
#make a second user
useradd -c "User B" -g tv -G writers,movie -m -s /bin/bash usr_b
passwd usr_b

#check who belongs to what group
grep <gid> /etc/passwd
```
