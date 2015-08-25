
## General
1. apg - generates several random passwords
2. corkscrew - tunelling
3. http://cntlm.sourceforge.net/ - NTLM/NTLM Session Response/NTLMv2 authenticating HTTP proxy

### Ubuntu
#### Autostart
`sudo update-rc.d -f postgresql remove`

#### Default
How to update alternatives for Linux Default Editor

`sudo update-alternatives --config editor`


#### GUI

CompizConfig Settings Manager call it as `ccsm` then choose:
```
Desktop->Ubuntu Unity Plugin
               ->Key to show the HUD when tapped
                <DISABLED>
```

### Redhat

    hostnamectl --static set-hostname oel7
    systemctl restart systemd-hostnamed
    
Get familiar with Network Manager CLI:

    nmcli -p g
    nmcli connection
    nmcli c show *connection-id*
    nmcli device show
    
http://www.certdepot.net/rhel7-get-started-nmcli/

Modify /etc/sysconfig/network-scripts/ifcfg* with DOMAIN="domain.com sub.domain.com"

#### RPM

[You've been told that working with RPMs needs system administrator privileges? You've been misled.](http://www.nordugrid.org/documents/rpm_for_everybody.html)

#### GUI

[Automatic Login](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Desktop_Migration_and_Administration_Guide/user-sessions.html#configuring-automatic-login)

    /etc/gdm/custom.conf
    [daemon]
    AutomaticLoginEnable=True
    AutomaticLogin=john

#### ls colors for black terminals

    /etc/profile.d/colorls.sh
    /etc/DIR_COLORS

https://lists.ubuntu.com/archives/kubuntu-users/2006-June/006626.html

#### YUM

in `/etc/yum.conf`:

    proxy=http://myproxy:80/
    proxy_username=myuser
    proxy_password=mypassword


    yum group list
    yum group install 'Server with GUI'
    yum group install 'Development Tools'


    rpm --httpproxy=user:pass@proxyhost --httpport=80 -Uvh \
      http://dl.fedoraproject.org/pub/epel/7/x86_64/e/epel-release-7-5.noarch.rpm
    rpm --httpproxy=user:pass@proxyhost --httpport=80 -Uvh \  
      http://rpms.famillecollet.com/enterprise/remi-release-7.rpm


    yum install oracle-rdbms-server-12cR1-preinstall

#### systemctl

    systemctl get-default
    systemctl set-default graphical.target
    systemctl list-unit-files
    systemctl disable microcode.service


#### GRUB

##### Default Kernel

[Customizing GRUB](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/System_Administrators_Guide/sec-Customizing_GRUB_2_Menu.html)

    [root@oel7 ~]# grub2-set-default 3
    [root@oel7 ~]# cat /boot/grub2/grubenv 
    
Note that the position of a menu entry in the list is denoted by a number starting with zero; therefore, in the example above, the third entry will be loaded. This value will be overwritten by the name of the next kernel to be installed. 

To force a system to always use a particular menu entry, use the menu entry name as the key to the GRUB_DEFAULT directive in the `/etc/default/grub` file. To list the available menu entries, run the following command as root:

    awk -F\' '$1=="menuentry " {print $2}' /etc/grub2.cfg
    
  
#### SVN
The standard svn included in RHEL7 does not support http and https schemes.
There is another svn from Wandisco prepared so the solution is to remove
Redhat delivered svn, exclude it from the repository and pick that one from Wandisco.
An extra repository (EPEL) is required to fully satisfy dependencies.
The story is mentioned in two following articles:

1. [Install Subversion 1.8.9](http://tecadmin.net/install-subversion-1-8-on-centos-rhel/)
2. [EPEL and REMI](http://tecadmin.net/install-epel-and-remi-repository-on-centos-and-redhat/)

#### GIT 
GIT missess SVN support with an error of `"Can't locate SVN/Core.pm in @INC"`. The missing
part is present in WandiscoSVN repository:

    yum --enablerepo=* install subversion-perl
