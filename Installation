Intro

This PROX installation section is describing the different steps that are needed to install PROX.

There is also a script available that can do this automatically for CentOS and that could be modified for the distribution you are using. This script is executing all steps mentioned below except for the binding of the module. The script is made to be used with the packer tool (for more info read the README. If you are NOT using the packer tool, you will have to copy a few more files that are used in this script as described in provisioners of centos.json.

If you are using the rapid scripts, this is all done automatically and you should skip this PROX installation chapter.

Prerequisites

DPDK must be installed prior to running make in the PROX directory. The README file shipped with PROX describes what versions of DPDK are supported, and if any patches are needed for the chosen DPDK version.

The following packages need to be installed. (Example for destributions that are using rpm)

sudo yum install numactl-devel net-tools wget gcc unzip libpcap-devel ncurses-devel libedit-devel pciutils lua-devel kernel-devel 
Jump Start


The following instructions are here to help customers to start using PROX. It's by no means a complete guide, for detailed instructions on how to install and use DPDK please refer to its documentation. Your mileage may vary depending on a particular Linux distribution and hardware in use.

Edit grub default configuration:

vi /etc/default/grub

Add the following to the kernel boot parameters

default_hugepagesz=1G hugepagesz=1G hugepages=8

Rebuild grub config and reboot the system:

grub2-mkconfig -o /boot/grub2/grub.cfg
reboot

Verify that hugepages are available

cat /proc/meminfo
...
HugePages_Total:  8
HugePages_Free:   8
Hugepagesize:     1048576 kB
...

Re-mount huge pages

mkdir -p /mnt/huge
umount `awk '/hugetlbfs/ { print $2 }' /proc/mounts` >/dev/null 2>&1
mount -t hugetlbfs nodev /mnt/huge/

Compile and build DPDK

Add the following to the end of ~/.bashrc file

export RTE_SDK=/root/dpdk
export RTE_TARGET=x86_64-native-linuxapp-gcc
export RTE_UNBIND=$RTE_SDK/tools/dpdk_nic_bind.py

Re-login or source that file

. ~/.bashrc

Build DPDK

git clone https://github.com/DPDK/dpdk
cd dpdk
git checkout v18.08
make install T=$RTE_TARGET


Bind modules

Load uio module

lsmod | grep -w "^uio" >/dev/null 2>&1 || sudo modprobe uio
sleep 1

Load igb_uio module

lsmod | grep -w "^igb_uio" >/dev/null 2>&1 || sudo insmod $RTE_SDK/$RTE_TARGET/kmod/igb_uio.ko

Discover network devices available on the system:

lspci | grep Ethernet

Prior launching PROX, ports that are to be used by it must be bound to the igb_uio driver.

The following command will bind all Intel® Ethernet Converged Network Adapter X710 ports to igb_uio:

lspci | grep X710 | cut -d' ' -f 1 | sudo xargs -I {} python2.7 $RTE_UNBIND --bind=igb_uio {}

The following command will bind all Intel® 82599 10 Gigabit Ethernet Controller ports to igb_uio:

lspci | grep 82599 | cut -d' ' -f 1 | sudo xargs -I {}  python2.7 $RTE_UNBIND --bind=igb_uio {}
Compiling and running PROX

Download and extract the PROX archive

git clone https://github.com/opnfv/samplevnf

cd samplevnf/VNFs/DPPD-PROX

git checkout origin/master

Build the PROX
make

The set of sample configuration files can be found in:

./config/*

PROX generation sample configs are in:

./gen/*

To launch PROX one may use the following command as an example, assuming the current directory is where you've just built PROX:

./build/prox -f ./config/handle_none.cfg
