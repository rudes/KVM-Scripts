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

VERSION="7 (wheezy)"

root@base:~# df -h

Filesystem                                              Size  Used Avail Use% Mounted on

rootfs                                                  1.8G  926M  816M  54% /

root@base:~# free -h

             total       used       free     shared    buffers     cached

Mem:          2.0G       156M       1.8G         0B       8.8M        68M

Swap:         132M         0B       132M

