#Networking#

##VPN##
###Socks Proxy###
[OpenSSH Cookbook - Proxies and Jump Hosts](https://en.wikibooks.org/wiki/OpenSSH/Cookbook/Proxies_and_Jump_Hosts)

    ssh -D 3555 server.example.org 
For example in Firefox, you'll also want the DNS requests to go via your proxy,
so changing `about:config` needs `network.proxy.socks_remote_dns` set to `true`.
You can tunnel samba over ssh, too.

A useful trick is "ssh -tt" which forces tty allocation:
   $ ssh -tt firewall.example.com ssh -tt server2.example.org
   
