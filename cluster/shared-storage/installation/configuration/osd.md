# OSD

Now we need to create OSD for each drive. On pve31, identify the disks in the system.

```
root@pve31:~# fdisk -l
Disk /dev/sda: 20 GiB, 21474836480 bytes, 41943040 sectors
Disk model: VMware Virtual S
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: gpt
Disk identifier: 0BC55AB0-6C8B-422F-A317-1BB53FB459AF

Device       Start      End  Sectors  Size Type
/dev/sda1       34     2047     2014 1007K BIOS boot
/dev/sda2     2048  1050623  1048576  512M EFI System
/dev/sda3  1050624 41943006 40892383 19.5G Linux LVM
```

I can see the original OS disk with three partitions. Further down I can see the three disks I created.

```
Disk /dev/sdb: 20 GiB, 21474836480 bytes, 41943040 sectors
Disk model: VMware Virtual S
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes


Disk /dev/sdc: 20 GiB, 21474836480 bytes, 41943040 sectors
Disk model: VMware Virtual S
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes


Disk /dev/sdd: 20 GiB, 21474836480 bytes, 41943040 sectors
Disk model: VMware Virtual S
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
```

The command **lsblk** shows this more clearly

```
root@pve31:~# lsblk
NAME               MAJ:MIN RM  SIZE RO TYPE MOUNTPOINTS
sda                  8:0    0   20G  0 disk 
├─sda1               8:1    0 1007K  0 part 
├─sda2               8:2    0  512M  0 part 
└─sda3               8:3    0 19.5G  0 part 
  ├─pve-swap       252:0    0  1.9G  0 lvm  [SWAP]
  ├─pve-root       252:1    0  8.8G  0 lvm  /
  ├─pve-data_tmeta 252:2    0    1G  0 lvm  
  │ └─pve-data     252:4    0  6.8G  0 lvm  
  └─pve-data_tdata 252:3    0  6.8G  0 lvm  
    └─pve-data     252:4    0  6.8G  0 lvm  
sdb                  8:16   0   20G  0 disk 
sdc                  8:32   0   20G  0 disk 
sdd                  8:48   0   20G  0 disk 
sr0                 11:0    1  1.5G  0 rom  
root@pve31:~# 
```

Now I create an OSD on pve31 for **/dev/sdb**

```
root@pve31:~# pveceph createosd /dev/sdb
create OSD on /dev/sdb (bluestore)
wiping block device /dev/sdb
200+0 records in
200+0 records out
209715200 bytes (210 MB, 200 MiB) copied, 0.221059 s, 949 MB/s
Running command: /bin/ceph-authtool --gen-print-key
Running command: /bin/ceph --cluster ceph --name client.bootstrap-osd --keyring /var/lib/ceph/bootstrap-osd/ceph.keyring -i - osd new 5d91149e-abfd-488a-bbab-2e4c7418419e
Running command: vgcreate --force --yes ceph-5e9d058e-1f60-429c-99e5-10fa54870e95 /dev/sdb
 stdout: Physical volume "/dev/sdb" successfully created.
 stdout: Volume group "ceph-5e9d058e-1f60-429c-99e5-10fa54870e95" successfully created
Running command: lvcreate --yes -l 5119 -n osd-block-5d91149e-abfd-488a-bbab-2e4c7418419e ceph-5e9d058e-1f60-429c-99e5-10fa54870e95
 stdout: Logical volume "osd-block-5d91149e-abfd-488a-bbab-2e4c7418419e" created.
Running command: /bin/ceph-authtool --gen-print-key
Running command: /bin/mount -t tmpfs tmpfs /var/lib/ceph/osd/ceph-0
--> Executable selinuxenabled not in PATH: /sbin:/bin:/usr/sbin:/usr/bin
Running command: /bin/chown -h ceph:ceph /dev/ceph-5e9d058e-1f60-429c-99e5-10fa54870e95/osd-block-5d91149e-abfd-488a-bbab-2e4c7418419e
Running command: /bin/chown -R ceph:ceph /dev/dm-5
Running command: /bin/ln -s /dev/ceph-5e9d058e-1f60-429c-99e5-10fa54870e95/osd-block-5d91149e-abfd-488a-bbab-2e4c7418419e /var/lib/ceph/osd/ceph-0/block
Running command: /bin/ceph --cluster ceph --name client.bootstrap-osd --keyring /var/lib/ceph/bootstrap-osd/ceph.keyring mon getmap -o /var/lib/ceph/osd/ceph-0/activate.monmap
 stderr: 2025-06-27T18:40:45.167+0100 70e741dac6c0 -1 auth: unable to find a keyring on /etc/pve/priv/ceph.client.bootstrap-osd.keyring: (2) No such file or directory
2025-06-27T18:40:45.167+0100 70e741dac6c0 -1 AuthRegistry(0x70e73c061620) no keyring found at /etc/pve/priv/ceph.client.bootstrap-osd.keyring, disabling cephx
 stderr: got monmap epoch 3
--> Creating keyring file for osd.0
Running command: /bin/chown -R ceph:ceph /var/lib/ceph/osd/ceph-0/keyring
Running command: /bin/chown -R ceph:ceph /var/lib/ceph/osd/ceph-0/
Running command: /bin/ceph-osd --cluster ceph --osd-objectstore bluestore --mkfs -i 0 --monmap /var/lib/ceph/osd/ceph-0/activate.monmap --keyfile - --osd-data /var/lib/ceph/osd/ceph-0/ --osd-uuid 5d91149e-abfd-488a-bbab-2e4c7418419e --setuser ceph --setgroup ceph
 stderr: 2025-06-27T18:40:45.374+0100 7aa39449b540 -1 bluestore(/var/lib/ceph/osd/ceph-0/) _read_fsid unparsable uuid
--> ceph-volume lvm prepare successful for: /dev/sdb
Running command: /bin/chown -R ceph:ceph /var/lib/ceph/osd/ceph-0
Running command: /bin/ceph-bluestore-tool --cluster=ceph prime-osd-dir --dev /dev/ceph-5e9d058e-1f60-429c-99e5-10fa54870e95/osd-block-5d91149e-abfd-488a-bbab-2e4c7418419e --path /var/lib/ceph/osd/ceph-0 --no-mon-config
Running command: /bin/ln -snf /dev/ceph-5e9d058e-1f60-429c-99e5-10fa54870e95/osd-block-5d91149e-abfd-488a-bbab-2e4c7418419e /var/lib/ceph/osd/ceph-0/block
Running command: /bin/chown -h ceph:ceph /var/lib/ceph/osd/ceph-0/block
Running command: /bin/chown -R ceph:ceph /dev/dm-5
Running command: /bin/chown -R ceph:ceph /var/lib/ceph/osd/ceph-0
Running command: /bin/systemctl enable ceph-volume@lvm-0-5d91149e-abfd-488a-bbab-2e4c7418419e
 stderr: Created symlink /etc/systemd/system/multi-user.target.wants/ceph-volume@lvm-0-5d91149e-abfd-488a-bbab-2e4c7418419e.service -> /lib/systemd/system/ceph-volume@.service.
Running command: /bin/systemctl enable --runtime ceph-osd@0
 stderr: Created symlink /run/systemd/system/ceph-osd.target.wants/ceph-osd@0.service -> /lib/systemd/system/ceph-osd@.service.
Running command: /bin/systemctl start ceph-osd@0
--> ceph-volume lvm activate successful for osd ID: 0
--> ceph-volume lvm create successful for: /dev/sdb
root@pve31:~# 
```

Now I do the same for /dev/sdc and /dev/sdd on each server.

At the end, I check to see what OSD I have and there identifiers.

```
root@pve32:~# ceph osd tree
ID  CLASS  WEIGHT   TYPE NAME       STATUS  REWEIGHT  PRI-AFF
-1         0.17537  root default                             
-3         0.05846      host pve31                           
 0    hdd  0.01949          osd.0       up   1.00000  1.00000
 1    hdd  0.01949          osd.1       up   1.00000  1.00000
 2    hdd  0.01949          osd.2       up   1.00000  1.00000
-7         0.05846      host pve32                           
 3    hdd  0.01949          osd.3       up   1.00000  1.00000
 5    hdd  0.01949          osd.5       up   1.00000  1.00000
 7    hdd  0.01949          osd.7       up   1.00000  1.00000
-5         0.05846      host pve33                           
 4    hdd  0.01949          osd.4       up   1.00000  1.00000
 6    hdd  0.01949          osd.6       up   1.00000  1.00000
 8    hdd  0.01949          osd.8       up   1.00000  1.00000
root@pve32:~# 
```

And through the GUI

<figure><img src="../../../../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

I could have done this through the GUI, but in earlier versions, it was a bit buggy.
