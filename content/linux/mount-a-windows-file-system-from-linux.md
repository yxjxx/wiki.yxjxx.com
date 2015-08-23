---
title: "MOUNT A WINDOWS FILE SYSTEM FROM LINUX"
date: 2015-08-23 18:11
---

***************
1. $su root
2. \#mkdir /mnt/win7 (mount is to set a inlet(a folder) of a file system)
3. \#mount -t ntfs /dev/sda2 /mnt/win7 (man mount to find what those parameters mean)
4. \#umount /mnt/win7 (umount)


*************************

mount it Automatically when startup
--------------------

1. edit /etc/fstab : add "/dev/sda2 /mnt/win7 ntfs defaults 0 0" after the last line (google "etc/fstab format" to make sense of the sentence)
2. test if it will work :

```
➜  /home/yxj  >df
Filesystem     1K-blocks    Used Available Use% Mounted on
/dev/sda8       37821092 5346220  30530604  15% /
none                   4       0         4   0% /sys/fs/cgroup
udev             5077160       4   5077156   1% /dev
tmpfs            1018360    1420   1016940   1% /run
none                5120       0      5120   0% /run/lock
none             5091788   18156   5073632   1% /run/shm
none              102400      24    102376   1% /run/user
/dev/sda5         274407   44366    211353  18% /boot
/dev/sda7       19553560 3366904  15170336  19% /home
➜  /home/yxj  >sudo mount -a
➜  /home/yxj  >df
Filesystem     1K-blocks      Used Available Use% Mounted on
/dev/sda8       37821092   5454492  30422332  16% /
none                   4         0         4   0% /sys/fs/cgroup
udev             5077160         4   5077156   1% /dev
tmpfs            1018360      1420   1016940   1% /run
none                5120         0      5120   0% /run/lock
none             5091788     18156   5073632   1% /run/shm
none              102400        24    102376   1% /run/user
/dev/sda5         274407     44366    211353  18% /boot
/dev/sda7       19553560   3366888  15170352  19% /home
/dev/sda2      419430396 323037652  96392744  78% /mnt/win7
➜  /home/yxj  >
```

/dev/sda2 mount successfully.

**************

---EOF---
