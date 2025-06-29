# Monitor

We need to create a monitor on each server, three is a normal number to create.

```
root@pve31:~# pveceph createmon
unable to get monitor info from DNS SRV with service name: ceph-mon
rados_connect failed - No such file or directory
creating new monitor keyring
creating /etc/pve/priv/ceph.mon.keyring
importing contents of /etc/pve/priv/ceph.client.admin.keyring into /etc/pve/priv/ceph.mon.keyring
monmaptool: monmap file /tmp/monmap
monmaptool: generated fsid d860aee2-3094-4a5b-889d-fbc991bb164f
setting min_mon_release = octopus
epoch 0
fsid d860aee2-3094-4a5b-889d-fbc991bb164f
last_changed 2025-06-27T18:25:32.203344+0100
created 2025-06-27T18:25:32.203344+0100
min_mon_release 15 (octopus)
election_strategy: 1
0: [v2:192.168.171.31:3300/0,v1:192.168.171.31:6789/0] mon.pve31
monmaptool: writing epoch 0 to /tmp/monmap (1 monitors)
created the first monitor, assume it's safe to disable insecure global ID reclaim for new setup
Configuring keyring for ceph-crash.service
Created symlink /etc/systemd/system/ceph-mon.target.wants/ceph-mon@pve31.service -> /lib/systemd/system/ceph-mon@.service.
creating manager directory '/var/lib/ceph/mgr/ceph-pve31'
creating keys for 'mgr.pve31'
setting owner for directory
enabling service 'ceph-mgr@pve31.service'
Created symlink /etc/systemd/system/ceph-mgr.target.wants/ceph-mgr@pve31.service -> /lib/systemd/system/ceph-mgr@.service.
starting service 'ceph-mgr@pve31.service'
root@pve31:~# 
```

If there is one monitor, we can interact with Ceph. Try getting the status.

```
root@pve31:~# ceph status
  cluster:
    id:     075e6985-ef31-445a-9f33-564610fdb5b7
    health: HEALTH_WARN
            OSD count 0 < osd_pool_default_size 3
 
  services:
    mon: 1 daemons, quorum pve31 (age 2m)
    mgr: pve31(active, since 2m)
    osd: 0 osds: 0 up, 0 in
 
  data:
    pools:   0 pools, 0 pgs
    objects: 0 objects, 0 B
    usage:   0 B used, 0 B / 0 B avail
    pgs:     
 
root@pve31:~# 
```

Create a monitor on each of the other pve.
