# Clones

Earlier, you created clones pve31, 32, 33

With basic Linux skills I can change configuration files manually and give these unique IPv4 addresses, names etc.

## Manual Changes

1. Edit **/etc/hostname**
2. Change the startup message in **/etc/issue**
3. Edit **/etc/network/interfaces**&#x20;
4. Change the IPv4 address and host name in **/etc/hosts** and add entries for all the servers.

```
127.0.0.1 localhost.localdomain localhost

192.168.171.31 pve31.buncrana.iotech.ie pve31
192.168.171.32 pve32.buncrana.iotech.ie pve32
192.168.171.33 pve33.buncrana.iotech.ie pve33

# The following lines are desirable for IPv6 capable hosts

::1     ip6-localhost ip6-loopback
fe00::0 ip6-localnet
ff00::0 ip6-mcastprefix
ff02::1 ip6-allnodes
ff02::2 ip6-allrouters
ff02::3 ip6-allhosts

```

Now perform tests to ensure the work has been created successfully.&#x20;
