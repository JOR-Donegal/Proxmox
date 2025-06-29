# Shared Storage

At the moment, we could run VMs and we could move them from server to server, but it would be slow. Whenever we have virtualization clusters, we have a shared storage technology. In VMWare, this is vSAN, in Hyper-V, Clustered Shared Storage.

In Proxmox, we use **Ceph**. This is an application which joins hard drives on local servers across a range of servers in the cluster, over the network. It allows for Software Defined Storage.

For reliable storage, we need at least 3 copies, but our capacity will be Total/3.&#x20;

Consider our three servers. Shut them down now and add three 20GB hard drives to each.

<figure><img src="../../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

Now restart the pve's.

If drive have been previously used, you need to wipe the first sectors and recreate a GPT entry. For example, to wipe /dev/sdb

```
dd if=/dev/zero of=/dev/sdb bs=1M count=200
ceph-disk zap /dev/sdb
```
