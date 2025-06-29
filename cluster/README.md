# Cluster

## Nomenclature

Clustering servers is the concept of connecting multiple servers such that they act as a highly available single system. If a single server fails, another server takes over its load. Each physical server associated with a cluster is a **node** and where we are using virtualization, will be called a **host**.&#x20;

We normally build cluster with an odd number of nodes. The **quorum** refers to the minimum number of nodes required for the cluster to operate and the term voting is often used. This ensures that the cluster remains operational and consistent even when some nodes fail or become unreachable. If communications fail to a node, the cluster is said to be **partitioned**. Two servers can still communicate and as they are two out of three of the resources, they have a majority vote. The isolated server knows that it is one out of three and ceases to carry out tasks. This prevents a **split-brain** occurring, when a cluster is partitioned into multiple independent groups, each believing it is the valid cluster.&#x20;

Quorum ensures only one group is active. It is possible to operate a cluster with an even number of nodes, we need to add a resource so there cannot be a tied vote. A **witness** disk on a file share can provide this tie-break. A two node cluster with a disk witness can continue operating if one node fails, as the disk witness provides the extra vote for quorum.

## Summary

To get the full functionality of a server, some sort of shared storage is normally used. This may be fibre channel, iSCSI or in recent times, built into the server operating system. Do some reading on

* Clustered Shared Storage (Microsoft)
* vSAN (VMWare)
* Ceph (Linux)

In this sequence, we are going to build a Proxmox cluster. I recommend building the cluster from fresh nodes with no VMs....nothing to break! For these exercises, I am using VMWare Workstation and created a gold Proxmox image with&#x20;

* 20GB root drive
* 3 \* 30 GB drives for ZFS
* First NIC as a bridged connection so I can manage ProxMox like a remote server on 192.168.5.0/24.
* Second NIC in LAN segment for cluster intercommunications on 192.168.251.0/24.
* Third NIC for Storage on 192.168.252.0/24.
* Fourth NIC for VMs. This would normally be a tagged connection on a real system, so I made this a LAN segment also.

Once it was built and interfaces configured and tested, I cloned this as three servers, Proxmox21, 22, 23.

You can't do that on bare metal, so when rolling out hosts in a commercial environment, consider [automating the installation](https://pve.proxmox.com/wiki/Automated_Installation) and configuration.
