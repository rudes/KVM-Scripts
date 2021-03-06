# KVM Scripts for Cloning Virtual Machines and Managing them.

## My Setup

### Host

	CentOS release 6.6 - Linux 2.6.32-504.16.2.el6.x86_64 GNU/Linux
	libvirt version: 0.10.2, package: 46.el6_6.6 (CentOS BuildSystem)

### Base Guest

```bash
	Debian GNU/Linux 7 (wheezy) - Linux base 3.2.0-4-amd64 x86_64 GNU/Linux

	Filesystem                  Size  Used Avail Use% Mounted on
	rootfs                      1.8G  926M  816M  54% /

								total       used       free     shared    buffers     cached
	Mem:          2.0G       156M       1.8G         0B       8.8M        68M
	Swap:         132M         0B       132M
```

### Scripts

exclonebase is used to clone a baseline VM, in my case i use it to clone a simple debian 2GB machine. exclonebase will clone the vm, resize the storage drive, activate the swap drive, and rename the new guest's hostname.

exchangehost is kept on the baseline guest VM and is used to change the hostname of the guest.

ckguestip will get the mac of each VM and compare it against the IP's on the network to give you a list of IP Addresses for your virtual machines.

### ckguestip Example
	GUEST1:      192.168.1.2    --  52:54:00:e8:ca:04
	GUEST2:      192.168.1.91   --  52:54:00:61:18:0b
	GUEST3:      192.168.1.191  --  52:54:00:db:63:d0
	GUEST4:      192.168.1.220  --  52:54:00:44:81:89
	GUEST5:      192.168.1.122  --  52:54:00:3e:12:94
	GUEST6:      192.168.1.109  --  52:54:00:0b:d1:51

exsyncpass is for syncing your ssh-keygens with your guest servers, if you set it with your base they will work on every VM, but if you ever need to refresh them this will make it easy.

### Installation

* Install [libvirt](http://libvirt.org/)
* Install [git](https://git-scm.com/)
* Setup a [Baseline VM](http://www.howtogeek.com/117635/how-to-install-kvm-and-create-virtual-machines-on-ubuntu/) (Ubuntu Tutorial, but it's all the same.)

Shutdown the Baseline VM

```bash
	virsh shutdown VMNAME
```

Cone the Repository

```bash
	git clone https://github.com/rudes/KVM-Scripts.git
	cd KVM-Scripts
```

Open the script and set your variables at the top

```bash
	vim exclonebase
```

Run and create your first clone!

```bash
	./exclonebase <VMNAME>
```

### Host Distributions Tested On

	Centos 6.6
	Debian 8.0
