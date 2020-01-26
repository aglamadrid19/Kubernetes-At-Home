# kumaster000 Configuration Docs
## OS
<pre>
<code># Hostname Configuration
<code>[root@kumas003 /]# cat /etc/centos-release</code>
<code>CentOS Linux release 8.1.1911 (Core)</code>

<code>[root@kumas003 /]# uname -a</code>
<code>Linux unknown0800278382A0 4.18.0-147.3.1.el8_1.x86_64 #1 SMP Fri Jan 3 23:55:26 UTC 2020 x86_64 x86_64 x86_64 GNU/Linux</code>
</pre>

## Network
<pre>
<code># ### Network Manager Service ###</code>
<code># Is NM running and enabled to start at boot?</code>
<code>[root@kumas003 /]# systemctl is-enabled NetworkManager<code>
<code>enabled<code>

<code>[root@kumas003 /]# systemctl is-active NetworkManager<code>
<code>active<code>
<code># ### MISSING VALIDATION ###<code>

<code># ### Network Interface Configuration ###</code>
<code># Configure enp0s3 static ip
<code>[root@kumas003 /]# nmcli c mod enp0s3 ipv4.method manual ipv4.addr "192.168.1.13/24"</code>

# Configure enp0s3 gateway
<code>[root@kumas003 /]# nmcli c mod enp0s3 ipv4.gateway "192.168.1.254"</code>

<code># Configure DNS Primary and Secondary</code>
<code>[root@kumas003 /]# nmcli con mod enp0s3 ipv4.dns "8.8.8.8"</code>
<code>[root@kumas003 /]# nmcli con mod enp0s3 ipv4.dns "1.1.1.1"</code>
<code># ### MISSING VALIDATION ###<code>

<code># ### Validation Example ###</code>
<code>[root@kumas003 /]# nmcli c show -a enp0s3 | grep ipv4.method</code>
<code>ipv4.method:manual</code>

<code># Reload enp0s3</code>
<code>[root@kumas003 /]# nmcli con up enp0s3</code>
</pre>

# 