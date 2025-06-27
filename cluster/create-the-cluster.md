---
description: From the command prompt
---

# Create the cluster

This task can be done from the GUI, but it more more precise and repeatable working from the CLI. To see the scope of the pvecm command, type

```
root@pve31:~# pvecm help
```

To create a cluster called **cluster1,** on **pve31** I run the command

```
root@pve31:~# pvecm create cluster1
Corosync Cluster Engine Authentication key generator.
Gathering 2048 bits for key from /dev/urandom.
Writing corosync key to /etc/corosync/authkey.
Writing corosync config to /etc/pve/corosync.conf
Restart corosync and cluster filesystem
root@pve31:~# 
```

Corosync is a messaging platform that allows cluster members to communicate, you can read about it [here](https://corosync.github.io/corosync/).

On **pve2** I run the following command to add **pve2** to the cluster on **pve1.**

```
root@pve32:~# pvecm add pve31
Please enter superuser (root) password for 'pve31': ********
Establishing API connection with host 'pve31'
The authenticity of host 'pve31' can't be established.
X509 SHA256 key fingerprint is 53:A4:11:FD:96:26:7A:80:68:41:3D:13:83:A6:2C:1D:9F:CA:6B:5D:F0:C2:B4:DF:7A:83:0B:FA:8E:53:E5:94.
Are you sure you want to continue connecting (yes/no)? yes
Login succeeded.
check cluster join API version
No cluster network links passed explicitly, fallback to local node IP '192.168.171.32'
Request addition of this node
Join request OK, finishing setup locally
stopping pve-cluster service
backup old database to '/var/lib/pve-cluster/backup/config-1751040031.sql.gz'
waiting for quorum...OK
(re)generate node files
generate new node certificate
merge authorized SSH keys
generated new node certificate, restart pveproxy and pvedaemon services
successfully added node 'pve32' to cluster.
root@pve32:~# 
```

I run the following command to check the status.

```
root@pve32:~# pvecm status
Cluster information
-------------------
Name:             cluster1
Config Version:   2
Transport:        knet
Secure auth:      on

Quorum information
------------------
Date:             Fri Jun 27 17:03:23 2025
Quorum provider:  corosync_votequorum
Nodes:            2
Node ID:          0x00000002
Ring ID:          1.9
Quorate:          Yes

Votequorum information
----------------------
Expected votes:   2
Highest expected: 2
Total votes:      2
Quorum:           2  
Flags:            Quorate 

Membership information
----------------------
    Nodeid      Votes Name
0x00000001          1 192.168.171.31
0x00000002          1 192.168.171.32 (local)
root@pve32:~# 
```

I repeat on pve3

```
root@pve33:~# pvecm add pve31
Please enter superuser (root) password for 'pve31': ********
Establishing API connection with host 'pve31'
The authenticity of host 'pve31' can't be established.
X509 SHA256 key fingerprint is 53:A4:11:FD:96:26:7A:80:68:41:3D:13:83:A6:2C:1D:9F:CA:6B:5D:F0:C2:B4:DF:7A:83:0B:FA:8E:53:E5:94.
Are you sure you want to continue connecting (yes/no)? yes
Login succeeded.
check cluster join API version
No cluster network links passed explicitly, fallback to local node IP '192.168.171.33'
Request addition of this node
Join request OK, finishing setup locally
stopping pve-cluster service
backup old database to '/var/lib/pve-cluster/backup/config-1751040332.sql.gz'
waiting for quorum...OK
(re)generate node files
generate new node certificate
merge authorized SSH keys
generated new node certificate, restart pveproxy and pvedaemon services
successfully added node 'pve33' to cluster.
root@pve33:~# 
```

And check the final status

```
root@pve33:~# pvecm status
Cluster information
-------------------
Name:             cluster1
Config Version:   3
Transport:        knet
Secure auth:      on

Quorum information
------------------
Date:             Fri Jun 27 17:06:46 2025
Quorum provider:  corosync_votequorum
Nodes:            3
Node ID:          0x00000003
Ring ID:          1.d
Quorate:          Yes

Votequorum information
----------------------
Expected votes:   3
Highest expected: 3
Total votes:      3
Quorum:           2  
Flags:            Quorate 

Membership information
----------------------
    Nodeid      Votes Name
0x00000001          1 192.168.171.31
0x00000002          1 192.168.171.32
0x00000003          1 192.168.171.33 (local)
root@pve33:~# 
```

Checking from the web interface

<figure><img src="../.gitbook/assets/image (29).png" alt=""><figcaption></figcaption></figure>

I need to up the memory per pve a bit!
