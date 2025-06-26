# Cluster

I recommend building the cluster from fresh nodes with no VMs....nothing to break! For these exercises, I am using VMWare Workstation and created a gold Proxmox image with&#x20;

* 20GB root drive
* 3 \* 30 GB drives for ZFS
* First NIC as a bridged connection so I can manage ProxMox like a remote server on 192.168.5.0/24.
* Second NIC in LAN segment for cluster intercommunications on 192.168.251.0/24.
* Third NIC for Storage on 192.168.252.0/24.
* Fourth NIC for VMs. This would normally be a tagged connection on a real system, so I made this a LAN segment also.

Once it was built and interfaces configured and tested, I cloned this as three servers, Proxmox21, 22, 23.

You can't do that on bare metal, so when rolling out hosts in a commercial environment, consider [automating the installation](https://pve.proxmox.com/wiki/Automated_Installation) and configuration.
