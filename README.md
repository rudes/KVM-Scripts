KVM Scripts for Cloning Virtual Machines and Managing them.

Read the Usage file for an example of the scripts being used live

Setup:

Host: 

CentOS release 6.6 - Linux 2.6.32-504.16.2.el6.x86_64 GNU/Linux
libvirtd --version:
		libvirt version: 0.10.2, package: 46.el6_6.6 (CentOS BuildSystem)

Base Guest:

root@base:~# uname -a
Linux base 3.2.0-4-amd64 #1 SMP Debian 3.2.68-1+deb7u1 x86_64 GNU/Linux

root@base:~# cat /etc/os-release
PRETTY_NAME="Debian GNU/Linux 7 (wheezy)"
NAME="Debian GNU/Linux"
VERSION_ID="7"
VERSION="7 (wheezy)"
ID=debian
ANSI_COLOR="1;31"
HOME_URL="http://www.debian.org/"
SUPPORT_URL="http://www.debian.org/support/"
BUG_REPORT_URL="http://bugs.debian.org/"

root@base:~# df -h
Filesystem                                              Size  Used Avail Use% Mounted on
rootfs                                                  1.8G  926M  816M  54% /
udev                                                     10M     0   10M   0% /dev
tmpfs                                                   202M  240K  202M   1% /run
/dev/disk/by-uuid/96182412-2aa9-43f4-a301-0e524b8a5d20  1.8G  926M  816M  54% /
tmpfs                                                   5.0M     0  5.0M   0% /run/lock
tmpfs                                                   430M     0  430M   0% /run/shm

root@base:~# free -h
             total       used       free     shared    buffers     cached
Mem:          2.0G       156M       1.8G         0B       8.8M        68M
-/+ buffers/cache:        79M       1.9G
Swap:         132M         0B       132M

