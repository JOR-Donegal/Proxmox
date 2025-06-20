# Bridge

Like with VMWare, there are several components to the network connection. A bridge (**vmbr**_**x**_) is assigned an IP address as a way for the kernel to interact. This then connects to one or more physical interfaces.

<figure><img src="../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

Proxmox uses Linux for its network stack, if you are familiar with Linux networking, this is easy. The configuration file is **/etc/network/interfaces**, however, Proxmox also uses an intermediate **/etc/network/interfaces.new** so that multiple changes can be made before committing.&#x20;

```
auto lo
iface lo inet loopback

iface ens33 inet manual

auto vmbr0
iface vmbr0 inet static
        address 192.168.146.11/24
        gateway 192.168.146.2
        bridge-ports ens33
        bridge-stp off
        bridge-fd 0


source /etc/network/interfaces.d/*
```

Looking at the user interface, I have configured four connections and this is

<figure><img src="../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

When you install Proxmox first, it will need a network interface for management. During the installation dialogue, you provide IPv4 information for this and it assigns to _**vmbr0**_.&#x20;
