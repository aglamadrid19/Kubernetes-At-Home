# kumaster000 Configuration Docs
## OS
<pre>
<code># Hostname Configuration</code>
<code>[root@kumas003 /]# hostnamectl set-hostname kumas003</code>

<code>[root@kumas003 /]# cat /etc/centos-release</code>
<code>CentOS Linux release 8.1.1911 (Core)</code>

<code>[root@kumas003 /]# uname -a</code>
<code>Linux kumas003 4.18.0-147.3.1.el8_1.x86_64 #1 SMP Fri Jan 3 23:55:26 UTC 2020 x86_64 x86_64 x86_64 GNU/Linux</code>
</pre>

## Network
<pre>
<code># ### Network Manager Service ###</code>
<code># Is NM running and enabled to start at boot?</code>
<code>[root@kumas003 /]# systemctl is-enabled NetworkManager</code>
<code>enabled</code>

<code>[root@kumas003 /]# systemctl is-active NetworkManager</code>
<code>active</code>
<code># ### MISSING VALIDATION ###</code>

<code># ### Network Interface Configuration ###</code>
<code># Configure enp0s3 static ip</code>
<code>[root@kumas003 /]# nmcli c mod enp0s3 ipv4.method manual ipv4.addr "192.168.1.13/24"</code>

<code># Configure enp0s3 gateway</code>
<code>[root@kumas003 /]# nmcli c mod enp0s3 ipv4.gateway "192.168.1.254"</code>

<code># Configure DNS Primary and Secondary</code>
<code>[root@kumas003 /]# nmcli con mod enp0s3 ipv4.dns "8.8.8.8"</code>
<code>[root@kumas003 /]# nmcli con mod enp0s3 ipv4.dns "1.1.1.1"</code>
<code># ### MISSING VALIDATION ###</code>

<code># ### Validation Example ###</code>
<code>[root@kumas003 /]# nmcli c show -a enp0s3 | grep ipv4.method</code>
<code>ipv4.method:manual</code>

<code># Reload enp0s3</code>
<code>[root@kumas003 /]# nmcli con up enp0s3</code>
</pre>

## SELinux
<pre>
<code># ### Disable SELinux Service ###</code>
<code>[root@kumas003 /]# sed -i 's/^SELINUX=.*/SELINUX=disabled/g' /etc/selinux/config</code>
<code>[root@kumas003 /]# reboot</code>
<code># ### MISSING VALIDATION ###</code>
</pre>

## Firewall
<pre>
<code># ### Firewalld Service ###</code>
<code># Is Firewalld running and enabled to start at boot?</code>
<code>[root@kumas003 /]# systemctl start firewalld</code>
<code>[root@kumas003 /]# systemctl enable firewalld</code>

<code># ### VALIDATION ###</code>
<code>[root@kumas003 /]# firewall-cmd --reload</code>
<code>[root@kumas003 /]# firewall-cmd --state</code>
<code>running</code>

<code># ### Basic Firewalld Configuration ###</code>
<code># Default zone = public</code>
<code>[root@kumas003 /]# firewall-cmd --set-default-zone=public</code>
<code>[root@kumas003 /]# firewall-cmd --reload</code>

<code># ### Default Allowed Services ###</code>
<code>[root@kumas003 /]# firewall-cmd --list-service --zone=public</code>
<code>cockpit dhcpv6-client ssh</code>
<code># ### MISSING VALIDATION ###</code>
</pre>

## Cockpit
<pre>
<code># ### Install Cockpit ###</code>
<code>[root@kumas003 /]# yum install -y cockpit</code>

<code># ### Cockpit Service ###</code>
<code>[root@kumas003 /]# systemctl enable --now cockpit.socket</code>
<code># ### MISSING VALIDATION ###</code>
</pre>

## Kuburnetes Cluster Config Setup
<pre>
<code># ### Unique Requirements ###</code>
<code># Unique MAC</code>
<code>[root@kumas003 /]# ip link</code>
<code># Unique Product-ID ###</code>
<code>[root@kumas003 /]# cat /sys/class/dmi/id/product_uuid</code>
<code># ### MISSING VALIDATION ###</code>
</pre>

<pre>
<code># ### Global ETC Hostfile ###</code>
<code># Backup original file</code>
<code>[root@kumas003 /]# cp /etc/hosts /etc/old.hosts</code>
<code># Global Hosts File Content</code>

<code># Localhost
<code>127.0.0.1   localhost localhost.localdomain localhost4 localhost4.localdomain4</code>

<code># Kubernetes Cluster Entries</code>
<code>192.168.1.13 kumas003</code>
<code>192.168.1.12 kunode002 kunode002-worker</code>
<code>192.168.1.11 kunode001 kunode001-worker</code>
<code># ### MISSING VALIDATION ###</code>
</pre>

## Docker-CE Installation
<pre>
<code># ### Docker-CE Installation ###</code>
<code># Install require packages</code>
<code>[root@kumas003 /]# sudo yum install -y yum-utils device-mapper-persistent-data lvm2</code>
<code># Install Docker-CE ###</code>
<code>[root@kumas003 /]# sudo yum install -y docker-ce --nobest</code>
<code># Start Docker at boot</code>
<code>[root@kumas003 /]# systemctl enable --now docker</code>
<code># ### MISSING VALIDATION ###</code>
</pre>
<pre>
<code># ### Docker-CE User Permissions ###</code>
<code># Add Management-User to docker group</code>
<code>[root@kumas003 /]# usermod -aG docker alamadrid</code>
<code># Verify changes</code>
<code>[root@kumas003 /]# id alamadrid</code>
<code># ### MISSING VALIDATION ###</code>
</pre>


