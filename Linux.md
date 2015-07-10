
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

#### RPM

[You've been told that working with RPMs needs system administrator privileges? You've been misled.](http://www.nordugrid.org/documents/rpm_for_everybody.html)

#### GUI

[Automatic Login](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Desktop_Migration_and_Administration_Guide/user-sessions.html#configuring-automatic-login)

    /etc/gdm/custom.conf
    [daemon]
    AutomaticLoginEnable=True
    AutomaticLogin=john

### GRUB

#### Default Kernel

[Customizing GRUB](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/System_Administrators_Guide/sec-Customizing_GRUB_2_Menu.html)

    [root@oel7 ~]# grub2-set-default 3
    [root@oel7 ~]# cat /boot/grub2/grubenv 
    
Note that the position of a menu entry in the list is denoted by a number starting with zero; therefore, in the example above, the third entry will be loaded. This value will be overwritten by the name of the next kernel to be installed. 

To force a system to always use a particular menu entry, use the menu entry name as the key to the GRUB_DEFAULT directive in the `/etc/default/grub` file. To list the available menu entries, run the following command as root:

    awk -F\' '$1=="menuentry " {print $2}' /etc/grub2.cfg
    
  
