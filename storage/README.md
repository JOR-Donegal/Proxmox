# Storage

The web interface is a bit clunky for managing storage. Its probably better to understand how to do this at the command prompt and how to edit the main configuration files. Before you begin, review [here](https://pve.proxmox.com/pve-docs/chapter-pvesm.html#_storage_types).

Proxmox support file storage and block storage. Thin provisioning is most suitable when learing using VMWare.

Take a look at /etc/pve/storage.cfg

```
dir: local
        path /var/lib/vz
        content backup,iso,vztmpl

lvmthin: local-lvm
        thinpool data
        vgname pve
        content images,rootdir
```
