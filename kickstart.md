#version=RHEL8
ignoredisk --only-use=sda

# Partition clearing information
clearpart --all --initlabel --drives=sda

# Use text based install
text

# Keyboard layouts
keyboard --vckeymap=us --xlayouts='us'

# System language
lang en_US.UTF-8

# Network information
network  --bootproto=static --device=enp0s3 --ip=192.168.1.10 --netmask=255.255.255.0 --gateway=192.168.1.254 --nameserver=8.8.8.8 --noipv6
network  --hostname=localhost.localdomain
# Root password
rootpw --iscrypted $6$ojpZdhZCHSvSaap.$H0ZoczJFiN4TjxW9rcHIG4R0AzP.N.tqDKmrfWAgW/V.i60bGg.eUNvKtJbCHLxPCJaFxhMRHhDI2D.BRDBQ6.
# Run the Setup Agent on first boot
firstboot --enable
# Do not configure the X Window System
skipx
# System services
services --enabled="chronyd"
# System timezone
timezone America/New_York --isUtc
url --url http://mirror.mia11.us.leaseweb.net/centos/8.1.1911/BaseOS/x86_64/os/
rootpw --iscrypted $6$qeBoJ.u4N3JF8BeS$0tD1cqKGH6HP/C6b6Vw9gN5CL9XlWwGAHypkz49.nyPKyfV5mJpbPvSmHea4Mgea1Jg6Nshu4hw2TO/URD3sp/
user --groups=wheel --name=alamadrid --password=$6$ABejKUdnpJqeEmlQ$xSkYUo8GZjVACOpcdLq8UsGMyZjzKr6J79AvGbZreEruMu/Uw9Tr0OVmQtGMN5AcDu6lMdRcGfv/DNO7eR.xi1 --iscrypted --gecos="Alvaro Lamadrid"
# Disk partitioning information
clearpart  --drives=sda
part pv.100 --fstype="lvmpv" --ondisk=sda --size=17436
part /boot --fstype="ext4" --ondisk=sda --size=1024
volgroup root-vg --pesize=4096 pv.100
logvol / --fstype="ext4" --grow --size=15000 --name=root-lv --vgname=root-vg
# SELinux disabled
selinux --disabled

# Reboot and eject media after installation
reboot --eject

%packages
@^Minimal Install
%end

%addon com_redhat_kdump --enable --reserve-mb='auto'
%end

%anaconda
%end