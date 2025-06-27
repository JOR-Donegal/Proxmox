# Networking

We always have a management interface, ideally two, feeding vmbr0.

One of my 10G interfaces connects to vmbr1 to tagged traffic to VMs.

One of my 10G interfaces is dedicated for storage.

With pve31, 32, 33 shut down, add network interfaces to each.

<figure><img src="../.gitbook/assets/image (27).png" alt=""><figcaption></figcaption></figure>

Adapter 2 connects to the LAN segment for tagged traffic.

Adapter 3 connects to the LAN segment for storage.

I set up as shown (pve33 for example).

<figure><img src="../.gitbook/assets/image (28).png" alt=""><figcaption></figcaption></figure>

My /etc/network/interfaces file looks like

```
auto lo
iface lo inet loopback

iface ens33 inet manual

iface ens37 inet manual

iface ens38 inet manual

auto vmbr0
iface vmbr0 inet static
        address 192.168.171.33/24
        gateway 192.168.171.2
        bridge-ports ens33
        bridge-stp off
        bridge-fd 0
        
auto vmbr1
iface vmbr1 inet manual
        bridge-ports ens37
        bridge-stp off
        bridge-fd 0
#Tagged traffic

auto vmbr2
iface vmbr2 inet manual
        bridge-ports ens38
        bridge-stp off
        bridge-fd 0
#Storage

source /etc/network/interfaces.d/*
```
