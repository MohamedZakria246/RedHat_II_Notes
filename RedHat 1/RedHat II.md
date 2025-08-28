
----> #Services 
----> #Security
----> #Storage

# Day1
System log
#Security 
1. Direct write (apache)
2. through systemd-Journal
3. rsyslog   ( vim /etc/rsyslog.conf )

to now the process and  fork
```bash
pstree -p
```

show the journal log from start machin
```bash 
journalctl --help
journalctl -n                  // for 10 line  -n3 to 3 line
journalctl -f

echo $$                      // to show the process id for this log 6795

journalctl --since 02:30:00 --until 03:30:00

journalctl _SYSTEMD_UNIT=NetworkManager.service 

journalctl _SYSTEMD_UNIT=sshd.service

```

rsyslog   ( vim /etc/rsyslog.conf )
```bash
 vim /etc/rsyslog.conf 
 
 *.info;mail.none;authpriv.none;cron.none                /var/log/messages


UDP 514
fac.serverity   @192.168.19.136

TCP 514
authpriv.*   @@912.168.19.136

```



```bash 
tty
#to shwitch user tty 
 chvt 3 
```

**Repository** 
```bash
#for install by old way
rpm -ivh tool.ver-release-arch.rpm



vim /etc/yum.repos.d/local.repo
		
```
**set data in repo 

```
[AppStream_local]
name=Local_AppStream
enable=1
baseurl=file://
gpgcheck=0
```
`

**to run and install all you need by local :-

```bash

vim /etc/yum.repos.d/local.repo 


[root@localhost ~]# cat /etc/yum.repos.d/local.repo 
[AppStream_local]
name=Local_AppStream
enable=1
baseurl=file:///run/media/zeko/CentOS-Stream-9-BaseOS-x86_64/AppStream/
gpgcheck=0


[BaseOS_Local]
name=Local_BaseOS
enable=1
baseurl=file:///run/media/zeko/CentOS-Stream-9-BaseOS-x86_64/BaseOS/
gpgcheck=0


# don't forgot to cloas all repo by go to : software >  RepoRepostory  > cloas

yum repolist 

yum list all


```

www.httpd.com

vsftpd

var

in clinte
fstream if httpd : //ip /AppStream 

# **Day 2**

Scheduling a Future Tasks in Linux:

1. One-Time Task
```bash
man at               # to show the help

[root@localhost ~]# at 9:28
warning: commands will be executed using /bin/sh
at> touch at_test         
at> <EOT>
job 1 at Mon Aug 25 09:28:00 2025                 #ctrl + D for out
[root@localhost ~]# 
```

```bash

[root@localhost ~]# at now+3min
warning: commands will be executed using /bin/sh
at> logger "Hello Hackers"
at> <EOT>
job 2 at Mon Aug 25 09:43:00 2025
[root@localhost ~]# 

# to show the achtion in another terminal
[root@localhost ~]# tail -f /var/log/messages 

[root@localhost ~]# at midnight Dec 31
warning: commands will be executed using /bin/sh
at> echo welcome > 2.txt
at> <EOT>
job 4 at Wed Dec 31 00:00:00 2025

```

2. recurring tasks with **cron 
	for do task more times 
```bash
crontab --help

crontab -e 



```

```
min      hour     day of month      Month    Day of week      |   command
0-59     0-23        1-31           1-12       0-6                 

* every  
sun-thr  range  من الاحد الى الخميس 
*/day  ده مره كل يومين


```

كل يوم الساعه 8  و نص الصبح  نبعت hello for user
```
0      8       *       *       *       echo "Hello" > /home/zeko/welcome.txt 
```


#### **anacrontab**

```bash
# to show the log for corn every 100M  or 7 day
 cat /var/log/cron
 
systemd-tmpfiles --clean

 du -hs /tmp
# 20K	/tmp

cat /usr/lib/tmpfiles.d/tmp.conf 


```

##### ACL in Linux

```bash
[root@localhost ~]# setfacl -m u:zeko:rw  at_test 
[root@localhost ~]# getfacl at_test 
# file: at_test
# owner: root
# group: root
user::rw-
user:zeko:rw-
group::r--
mask::rw-
other::r--

[root@localhost ~]# ll
total 4
-rw-------. 1 root root 996 Aug 24 08:56 anaconda-ks.cfg
-rw-rw-r--+ 1 root root   0 Aug 25 09:28 at_test


setfacl -b at_test       # for delete the ACL for the dir

```

### #Security 

Security-Enhanced Linux (SELinux) is ==a Linux kernel security module that provides mandatory access control (MAC) to enhance system security==.

Note: tow mode in SELinux
1. enforcing : prevention at login   and Logs violations
2. permissive : logs violations only (all of it -> messages)
3. disabled: naaah
when switching between them u have to reboot the machine 
```bash
ps -auxZ                # to show the Nabors for processes
```

open index and write data for test 
```bash
vim /var/www/html/index.html

[root@localhost ~]# getenforce    
Enforcing


```


show the enforcing
```bash
cat /etc/selinux/config
# SELINUX= can take one of these three values:
#     enforcing - SELinux security policy is enforced.
#     permissive - SELinux prints warnings instead of enforcing.
#     disabled - No SELinux policy is loaded.

SELINUX=enforcing
# SELINUXTYPE= can take one of these three values:
#     targeted - Targeted processes are protected,
#     minimum - Modification of targeted policy. Only selected processes are protected.
#     mls - Multi Level Security protection.
SELINUXTYPE=targeted

```

need this in password recovery

```bash
oot@localhost ~]# setenforce 0   
[root@localhost ~]# chcon -t test_t /var/www/html/index.html 


[root@localhost ~]# setenforce 1
[root@localhost ~]# restorecon /var/www/html/index.html 
[root@localhost ~]# ll -Z /var/www/html/index.html 
-rw-r--r--. 1 root root system_u:object_r:httpd_sys_content_t:s0 38 Aug 25 14:33 /var/www/html/index.html

```



# Day 3
Firewall :
	mask > is to throw unwanted deamon in / bev/null
	firewall > is the first statefull
	```


```bash
	firewall-cmd --set-default-zone=
```



add  ssh , tcp , dns , ftp , vnc-server , dmz , apache 

```bash
firewall-cmd  --zone=dmz  --add-service=http --add-service=dns --add-service=vnc-server   --add-service=ssh 
```


port
```bash
firewall-cmd  --add-port=10000/tcp

firewall-cmd --list-all

```




storage 

```
SATA , SAS  , USB Storage               /dev/sda , /dev/sdb 
NVMe (Many types of SSD)                /dev/nvme0  , /dev/nvme1 
Virtual Disk                            /dev/vda  ,   /dev/vdb
CD  , DVD                               /dev/sr0 ......sr1
SD , eMMc                               /dev/mmblk0 ....
```

```bash

lsblk                #to show the stordge
fdisk -l

```

| Feature        | **MBR**                          | **GPT**                      |
| -------------- | -------------------------------- | ---------------------------- |
| Max Disk Size  | 2 TB                             | 9.4 ZB (theoretical)         |
| Max Partitions | 4 primary (or 3 + 1 extended)    | 128 (no need for extended)   |
| Boot Mode      | Legacy BIOS                      | UEFI                         |
| Reliability    | Single partition table (fragile) | Multiple copies + CRC checks |
| Age / Usage    | Old, legacy systems              | Modern, recommended          |



```bash 

fdisk /dev/sdb

partprobe /dev/sdb

mkfs.ext4 /dev/sdb1 

mkdir media

mount /dev/sdb1  ./media/

 ls ./media/
	lost+found

df -h

```


LVM  is ==a flexible storage management system, primarily in Linux, that adds an abstraction layer over physical storage to allow dynamic resizing, spanning multiple disks, and other advanced features not possible with traditional partitioning==.

%% logical volume support for increase space %% 


# Day 4

Storage



add storage 7G  , 
```
[root@localhost ~]# lsblk
NAME      MAJ:MIN RM  SIZE RO TYPE MOUNTPOINTS
sda         8:0    0   25G  0 disk 
├─sda1      8:1    0    1G  0 part /boot
└─sda2      8:2    0   24G  0 part 
  ├─cs-root
  │       253:0    0 21.9G  0 lvm  /
  └─cs-swap
          253:1    0  2.1G  0 lvm  [SWAP]
sdb         8:16   0   10G  0 disk 
├─sdb1      8:17   0    2G  0 part 
└─sdb2      8:18   0    1K  0 part 
sdc         8:32   0    7G  0 disk 
sdd         8:48   0    5G  0 disk 
sr0        11:0    1  8.8G  0 rom  /run/media/zeko/CentOS-Stream-9-BaseOS-x86_64


```


```bash
gdisk /dev/sdc

partprobe /dev/sdc

fdisk >> n >> tl >> L > 8E              # L : to 

pvcreate /dev/sdc1  /dev/sdc2  /dev/sdd1


vgcreate VG1 /dev/sdc1 /dev/sdc2  /dev/sdd1

[root@localhost ~]# pvs
  PV         VG  Fmt  Attr PSize   PFree 
  /dev/sda2  cs  lvm2 a--  <24.00g     0 
  /dev/sdc1  VG1 lvm2 a--   <3.00g <3.00g
  /dev/sdc2  VG1 lvm2 a--   <4.00g <4.00g
  /dev/sdd1  VG1 lvm2 a--   <3.00g <3.00g

du -sh 

vgdisplay


```


LV :

```
lvs
lvcreat --help

lvcreate --size 1G  --name Lv1   VG1 

lvcreate --size 100M  --name Lv2  VG1 



```



```
mkfs.ext4 /dev/mapper/VG1-LV1

mkfs.xfs /dev/mapper/VG1-Lv2

df

mkdire media1 , media2
mount /dev/VG1/Lv1 media1
mount /dev/VG1/Lv2 media2

```



##### How to Extend The Volume Size ?

```bash
pvcreat /dev/sdc2
vgextend VG1 /dev/sdc2
lvextend -L +3G  /dev/VG1/LV1
xfs_growfs /dev/VG1/LV1
OR
resize2fs  /dev/VG1/LV1

OR
lvextend  -r -L +3G /dev/VG1/Lv1

```


##### How to Reduce the Volume size ? 

```bash
umount my_Data1
lvreduce -r -L -3G  /dev/VG1/lv1
vgreduce VG1 /dev/sdc2
prrmove /dev/sdc2

```


##### How to Remove the Volume?

```bash
umount my_Data1 my_Data2
lvremove /dev/VG1/Lv1

lvremove /dev/VG1/Lv2
vgremove VG1
pvremove /dev/sdc1 sdc3 sdb6 ....
```

|Task
extend storage 10GB





