# This is the second page to the lvm introduction in lvm.txt.

> LVM is an abstraction that provides virtualized environments for diskspace usage. This allows us to pool fragmented disk space into logical groups, that aggregate as one single disk pool. This then gets broken up into smaller partitions called Logical volume groups, acting as virtualized disk partitions.

> If we allocate more storage space or another disk to the overall storage space, we can partition those into seperate storage containers. Or, we would just add the entire disk to Volume Group.

## Show partitions and their respective types. 
command: ```lsblk```

## Create a physical volume from disk:
command: ```pvcreate /dev/<disk>```
> (this is done on a newly created disk added to the system)

## Remove a physical volume from disk: 
command: ```pvremove /dev/<disk>```

## Show all physical volumes on the system: 
command: ```pvs```

---

# Volume Groups: 
> These are gruops in which we can add one or more physical volumes **to**
> 
> These are gruops in which we can add one or more logical volumes **on**

## Create a Volume Group: 
command: ```vgcreate -s 8m <vg name> /dev/<disk>```
> (-s = physical extent size)

## List Volume Groups: 
command: ```vgs```

## Add a device to the volume group:
command: ```vgextend <volume group name> /dev/<disk>```

## Remove devices from the volume groups:
command: ```vgreduce <volume group name> /dev/sda```

## Delete the volume group: 
command: ```vgremove <volume group name>```




---

# Logical Volumes:
Logical volumes can be added to volume groups as partitions.

## Creating a Logical Volume: 
command: ```lvcreate --size <size> --name <lv name> <volume group name>``` 

## List Logical Volumes: 
command: ```lvs```
> or 
1. command: ```cd /dev/<volume group name>/ (check the directory of install)```
2. command: ```ls (whatever files in here are a logical volume link)```

## Removing Logical Volumes: 
command: ```lvremove /dev/<vg name>/<logical volume name>```





## Extending Logical Volumes: 
command: ```lvextend --size +<size><G,M> -r /dev/<path to logical volume>```

## Reducing the Logical Volumes: 
command: ```lvreduce --size +<size><G,M> -r /dev/<path to logical volume>```
> or
command: ```lvresize -L <size> -r /dev/<path to logical volume>```

**Note**: 
> For xfs file systems, we need to unmount the file system and create a new one with an appropriate size and remount it as appropriate.



**For notes on mounting a file system, refer to ../Mounting_FileSystems/mounting_filesystems.txt**

