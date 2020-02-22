# PR PXE 001 Configuration Docs
## Hypervisor Tools (VirtualBox)
<pre>
<code># ### Install VBox VM Tools dependencies</code>
<code># Epel repos</code>
<code>[root@kumas003 /]# dnf install https://dl.fedoraproject.org/pub/epel/epel-release-latest-8.noarch.rpm</code>
<code># ### MISSING VALIDATION ###</code>

<code># Packages to build kernel</code>
<code>[root@kumas003 /]# dnf install yum install gcc kernel-devel kernel-headers dkms make bzip2 perl</code>
<code># ### MISSING VALIDATION ###</code>

<code># Add KERN_DIR env var</code>
<code>[root@kumas003 /]# KERN_DIR=/usr/src/kernels/`uname -r`</code>
<code># ### MISSING VALIDATION ###</code>

<code># Run install script</code>
</pre>