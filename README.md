##########################################################################################

The Basics:

##########################################################################################

[root@host ~]# ./clonebase

######### Specify your new VM Name #######
New VM Name: CRYWEB02

######### Script will clone the base vm set in the script #########
Cloning Baseline VM
Allocating 'CRYWEB02.img'                                             | 2.0 GB     00:36

Clone 'CRYWEB02' created successfully.
Clone Complete

######### Starts the VM and get's the IP #########
Starting CRYWEB02
Domain CRYWEB02 started

Getting CRYWEB02's IP
CRYWEB02's IP: 192.168.1.109

######### Asks you if you'd like to increase the base storage to the VM #########
Storage Size: 2.0G
######### You NEED the + sign #########
Add Storage? (ex: +10G or 'n' to exit): +10G

Domain CRYWEB02 is being shutdown

Image resized.

######### Instructions on how to repartition the drives #########

##############################################################
# Entering SSH as root to Resize Storage and Change Hostname #
# Run fdisk /dev/vda                                         #
# Delete all partitions and rebuild with the extra storage   #
# Write the Changes                                          #
# Exit SSH to Reboot CRYWEB02                                #
##############################################################
Domain CRYWEB02 started

root@192.168.1.109's password:
Linux base 3.2.0-4-amd64 #1 SMP Debian 3.2.68-1+deb7u1 x86_64

The programs included with the Debian GNU/Linux system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Debian GNU/Linux comes with ABSOLUTELY NO WARRANTY, to the extent
permitted by applicable law.
Last login: Tue Apr 28 18:11:49 2015 from 192.168.1.21

######### If you don't know how to use fdisk you can use whatever you know or look up a coupl tutorials #########
######### There's a lot to fdisk, this is just a super basic repartition #########

root@base:~# fdisk /dev/vda

Command (m for help): p

Disk /dev/vda: 12.8 GB, 12834570240 bytes
16 heads, 63 sectors/track, 24868 cylinders, total 25067520 sectors
Units = sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disk identifier: 0x000d8c3b

   Device Boot      Start         End      Blocks   Id  System
/dev/vda1   *        2048     3819519     1908736   83  Linux
/dev/vda2         3821566     4093951      136193    5  Extended
/dev/vda5         3821568     4093951      136192   82  Linux swap / Solaris

Command (m for help): d
Partition number (1-5): 1

Command (m for help): d
Partition number (1-5): 2

Command (m for help): n
Partition type:
   p   primary (0 primary, 0 extended, 4 free)
   e   extended
Select (default p):
Using default response p
Partition number (1-4, default 1):
Using default value 1
First sector (2048-25067519, default 2048):
Using default value 2048
Last sector, +sectors or +size{K,M,G} (2048-25067519, default 25067519): 24795135

Command (m for help): n
Partition type:
   p   primary (1 primary, 0 extended, 3 free)
   e   extended
Select (default p): e
Partition number (1-4, default 2):
Using default value 2
First sector (24795136-25067519, default 24795136):
Using default value 24795136
Last sector, +sectors or +size{K,M,G} (24795136-25067519, default 25067519):
Using default value 25067519

Command (m for help): n
Partition type:
   p   primary (1 primary, 1 extended, 2 free)
   l   logical (numbered from 5)
Select (default p): l
Adding logical partition 5
First sector (24797184-25067519, default 24797184):
Using default value 24797184
Last sector, +sectors or +size{K,M,G} (24797184-25067519, default 25067519):
Using default value 25067519

Command (m for help): a
Partition number (1-5): 1

Command (m for help): t
Partition number (1-5): 5
Hex code (type L to list codes): 82
Changed system type of partition 5 to 82 (Linux swap / Solaris)

Command (m for help): p

Disk /dev/vda: 12.8 GB, 12834570240 bytes
16 heads, 63 sectors/track, 24868 cylinders, total 25067520 sectors
Units = sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disk identifier: 0x000d8c3b

   Device Boot      Start         End      Blocks   Id  System
/dev/vda1   *        2048    24795135    12396544   83  Linux
/dev/vda2        24795136    25067519      136192    5  Extended
/dev/vda5        24797184    25067519      135168   82  Linux swap / Solaris

Command (m for help): w
The partition table has been altered!

Calling ioctl() to re-read partition table.

WARNING: Re-reading the partition table failed with error 16: Device or resource busy.
The kernel still uses the old table. The new table will be used at
the next reboot or after you run partprobe(8) or kpartx(8)
Syncing disks.
root@base:~# logout
Connection to 192.168.1.109 closed.
Domain CRYWEB02 is being rebooted

Waiting for CRYWEB02 to reboot.
Expanding new storage

######### After reboot it will run resize2fs on /dev/vda1 #########
root@192.168.1.109's password:
resize2fs 1.42.5 (29-Jul-2012)
Filesystem at /dev/vda1 is mounted on /; on-line resizing required
old_desc_blocks = 1, new_desc_blocks = 1
Performing an on-line resize of /dev/vda1 to 3099136 (4k) blocks.
The filesystem on /dev/vda1 is now 3099136 blocks long.

######### Specify the hostname for the new box #########

New Hostname: CRYWEB02

root@192.168.1.109's password:
Removing Old Hostname Line from /etc/hosts
Ammending New Hostname Line to /etc/hosts
127.0.0.1       localhost

# The following lines are desirable for IPv6 capable hosts
::1     localhost ip6-localhost ip6-loopback
ff02::1 ip6-allnodes
ff02::2 ip6-allrouters
127.0.1.1       CRYWEB02.cryocorp.local CRYWEB02
Setting Hostname in /etc/hostname
CRYWEB02
Restarting VM
Waiting for CRYWEB02 to reboot.

######### You can add it to the /etc/hosts file on the host machine #########
######### so you can ssh with the hostname instead of IP #########

Add CRYWEB02 to /etc/hosts?: y
cat /etc/hosts

127.0.0.1   localhost localhost.localdomain localhost4 localhost4.localdomain4
::1         localhost localhost.localdomain localhost6 localhost6.localdomain6
192.168.1.21 host.cryocorp.co host

192.168.1.109   CRYWEB02

CRYWEB02 Ready to Go! at 192.168.1.109

######### Test out your new VM and set it up for your needs! #########

[root@host ~]# ssh cryweb02
The authenticity of host 'cryweb02 (192.168.1.109)' can't be established.
RSA key fingerprint is 90:df:f9:f3:00:cc:c3:8a:65:41:51:df:df:a3:9f:84.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added 'cryweb02' (RSA) to the list of known hosts.

root@cryweb02's password:
Linux CRYWEB02 3.2.0-4-amd64 #1 SMP Debian 3.2.68-1+deb7u1 x86_64

The programs included with the Debian GNU/Linux system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Debian GNU/Linux comes with ABSOLUTELY NO WARRANTY, to the extent
permitted by applicable law.
Last login: Wed Apr 29 15:41:59 2015 from 192.168.1.21
root@CRYWEB02:~# logout
Connection to cryweb02 closed.

##########################################################################################

[root@host ~]# ./getvmip

vm1: 192.168.1.63  --  52:54:00:3e:d7:81
vm2: 192.168.1.220  --  52:54:00:44:81:89
vm3: 192.168.1.122  --  52:54:00:3e:12:94
vm4: 192.168.1.109  --  52:54:00:0b:d1:51

######### getvmip is very simple, it generates a list of vm's from virsh, #########
######### takes their mac addresses and compares them against arp to get you the IP, #########
######### great for setting up new VM's when you don't have access to virt-viewer #########

##########################################################################################
