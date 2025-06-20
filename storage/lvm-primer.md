---
description: Logical Volume Manager
---

# LVM Primer

Disks are physical devices.

We can also have logical devices like partitins, which are subdivisions of a disk. But it doesn't have to be this way. We could aggregate disks together to get certain properties (performance, availability, size) and this is what we do with RAID controllers.&#x20;

<figure><img src="../.gitbook/assets/image (40).png" alt=""><figcaption></figcaption></figure>

Most operating system implement some form of logical volume manager (LVM) to abstract the storage from the requirements of the operating system A physical volume (PV) used to be a hard drive, but on a modern system it could be a partition, or it could be a concatenation of drives. It could also be presented as a logical unit number (LUN) of a remote storage array The physical volume will probably store data in sectors but these sectors are normally too small for optimal usage by the operating system. Sectors will be aggregated into blocks/clusters. Blocks might be aggregated into physical extents (PE), a contiguous area of storage. The PEs aggregate to form a volume group or VG and a volume group can be resized dynamically by adding new PVs.

<figure><img src="../.gitbook/assets/image (41).png" alt=""><figcaption></figcaption></figure>

The OS will be presented with logical extents (LEs). These may map directly to PEs or more complex arrangements may exist. For example, we sometimes mirror data to two disks for high availability. In this case, we might have a single LE map to two discrete PEs on separate PVs. Virtual partitions can be created from LEs called logical volumes or LVs. LVs can be expanded by adding new LEs to them. LVs can be moved from PV to PV as required. Software RAID allows us to make some very beneficial use of this flexibility.

To view the LVs on a system, use the command **lvdisplay**.

```
root@proxmox2:/dev/pve# lvdisplay
  --- Logical volume ---
  LV Name                data
  VG Name                pve
  LV UUID                S80BoN-F4o1-Qtlq-TKn3-oRTz-XVOS-0NZyCi
  LV Write Access        read/write
  LV Creation host, time proxmox, 2024-08-02 10:07:08 +0100
  LV Pool metadata       data_tmeta
  LV Pool data           data_tdata
  LV Status              available
  # open                 0
  LV Size                6.55 GiB
  Allocated pool data    0.00%
  Allocated metadata     1.57%
  Current LE             1678
  Segments               1
  Allocation             inherit
  Read ahead sectors     auto
  - currently set to     256
  Block device           252:6

  --- Logical volume ---
  LV Path                /dev/pve/swap
  LV Name                swap
  VG Name                pve
  LV UUID                S5l18a-ePna-bIGO-TQfg-AVQz-T8xy-02Dgos
  LV Write Access        read/write
  LV Creation host, time proxmox, 2024-08-02 10:07:07 +0100
  LV Status              available
  # open                 2
  LV Size                <2.38 GiB
  Current LE             608
  Segments               1
  Allocation             inherit
  Read ahead sectors     auto
  - currently set to     256
  Block device           252:2

  --- Logical volume ---
  LV Path                /dev/pve/root
  LV Name                root
  VG Name                pve
  LV UUID                JuEphc-HzIv-RZ7m-PXef-JW5d-vTMV-VzTeEu
  LV Write Access        read/write
  LV Creation host, time proxmox, 2024-08-02 10:07:08 +0100
  LV Status              available
  # open                 1
  LV Size                <8.56 GiB
  Current LE             2191
  Segments               1
  Allocation             inherit
  Read ahead sectors     auto
  - currently set to     256
  Block device           252:3
```

I can use **lvcreate** and **lvresize** as well. A bit risky on a live system, but feel free to play with these commands on a Proxmox VM.
