# Ceph

At the moment, we could run VMs and we could move them from server to server, but it would be slow. Whenever we have virtualization clusters, we have a shared storage technology. In VMWare, this is vSAN, in Hyper-V, Clustered Shared Storage.

In Proxmox, we use Ceph. This is an application which joins hard drives on local servers across a range of servers in the cluster, over the network.

For reliable storage, we need at least 3 copies. Consider our three servers. Shut them down now and add three hard drives to each.

<figure><img src=".gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>
