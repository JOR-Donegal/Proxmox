# Cluster File System

When we created the cluster, we also created a cluster file system (CFS), mounted at **/etc/pve** and this will be synchronized on each server using Corosync.

```
root@pve31:~# cd /etc/pve
root@pve31:/etc/pve# ls -l
total 4
-rw-r----- 1 root www-data  451 Jun 27 11:05 authkey.pub
-rw-r----- 1 root www-data  544 Jun 27 17:05 corosync.conf
-rw-r----- 1 root www-data   16 Jun 27 11:05 datacenter.cfg
drwxr-xr-x 2 root www-data    0 Jun 27 11:05 firewall
drwxr-xr-x 2 root www-data    0 Jun 27 11:05 ha
lrwxr-xr-x 1 root www-data    0 Jan  1  1970 local -> nodes/pve31
lrwxr-xr-x 1 root www-data    0 Jan  1  1970 lxc -> nodes/pve31/lxc
drwxr-xr-x 2 root www-data    0 Jun 27 11:05 mapping
drwxr-xr-x 2 root www-data    0 Jun 27 11:05 nodes
lrwxr-xr-x 1 root www-data    0 Jan  1  1970 openvz -> nodes/pve31/openvz
drwx------ 2 root www-data    0 Jun 27 11:05 priv
-rw-r----- 1 root www-data 2074 Jun 27 11:05 pve-root-ca.pem
-rw-r----- 1 root www-data 1704 Jun 27 11:05 pve-www.key
lrwxr-xr-x 1 root www-data    0 Jan  1  1970 qemu-server -> nodes/pve31/qemu-server
drwxr-xr-x 2 root www-data    0 Jun 27 11:05 sdn
-rw-r----- 1 root www-data  127 Jun 27 11:05 storage.cfg
-rw-r----- 1 root www-data   39 Jun 27 11:05 user.cfg
drwxr-xr-x 2 root www-data    0 Jun 27 11:05 virtual-guest
-rw-r----- 1 root www-data  119 Jun 27 11:05 vzdump.cron
root@pve31:/etc/pve# 
```

Check the other two servers, the files should be exactly the same. These are the cluster's configuration files. Test this by creating a dummy file on **pve1/etc/pve**

```
root@pve31:/etc/pve# echo "Yoo hoo 27JUN25" >> rubbish.txt
root@pve31:/etc/pve# ls -l
total 5
-rw-r----- 1 root www-data  451 Jun 27 11:05 authkey.pub
-rw-r----- 1 root www-data  544 Jun 27 17:05 corosync.conf
-rw-r----- 1 root www-data   16 Jun 27 11:05 datacenter.cfg
drwxr-xr-x 2 root www-data    0 Jun 27 11:05 firewall
drwxr-xr-x 2 root www-data    0 Jun 27 11:05 ha
lrwxr-xr-x 1 root www-data    0 Jan  1  1970 local -> nodes/pve31
lrwxr-xr-x 1 root www-data    0 Jan  1  1970 lxc -> nodes/pve31/lxc
drwxr-xr-x 2 root www-data    0 Jun 27 11:05 mapping
drwxr-xr-x 2 root www-data    0 Jun 27 11:05 nodes
lrwxr-xr-x 1 root www-data    0 Jan  1  1970 openvz -> nodes/pve31/openvz
drwx------ 2 root www-data    0 Jun 27 11:05 priv
-rw-r----- 1 root www-data 2074 Jun 27 11:05 pve-root-ca.pem
-rw-r----- 1 root www-data 1704 Jun 27 11:05 pve-www.key
lrwxr-xr-x 1 root www-data    0 Jan  1  1970 qemu-server -> nodes/pve31/qemu-server
-rw-r----- 1 root www-data   16 Jun 27 17:27 rubbish.txt
drwxr-xr-x 2 root www-data    0 Jun 27 11:05 sdn
-rw-r----- 1 root www-data  127 Jun 27 11:05 storage.cfg
-rw-r----- 1 root www-data   39 Jun 27 11:05 user.cfg
drwxr-xr-x 2 root www-data    0 Jun 27 11:05 virtual-guest
-rw-r----- 1 root www-data  119 Jun 27 11:05 vzdump.cron
root@pve31:/etc/pve# 

```

Now verify the same file is in **/etc/pve** on the other two server.&#x20;

A VM consists of a configuration file, and a related virtual hard drive, the image. When you create a VM, the configuration file is saved to the CFS. However, we still need shared storage for the disk image.

