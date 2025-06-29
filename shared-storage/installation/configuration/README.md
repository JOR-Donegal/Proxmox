# Configuration

On _one server only_, initialize Ceph. We need to tell it what network we are operating on.&#x20;

```
root@pve31:~# pveceph init --network 192.168.171.0/24
```

Check to see that the Ceph configuration file has been created.

```
root@pve31:~# more /etc/pve/ceph.conf 
[global]
        auth_client_required = cephx
        auth_cluster_required = cephx
        auth_service_required = cephx
        cluster_network = 192.168.171.0/24
        fsid = 075e6985-ef31-445a-9f33-564610fdb5b7
        mon_allow_pool_delete = true
        osd_pool_default_min_size = 2
        osd_pool_default_size = 3
        public_network = 192.168.171.0/24

[client]
        keyring = /etc/pve/priv/$cluster.$name.keyring
```

This is replicated to all servers in the cluster.
