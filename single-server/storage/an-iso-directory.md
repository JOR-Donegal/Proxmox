# An ISO directory

Do this exercise on a VM instance only, for training. If you are working on bare metal, this needs to be done in a more structured way.

I have added a second disk to my VM and verified that it shows up as **/dev/sdb**.

<figure><img src="../../.gitbook/assets/image (2) (1) (1).png" alt=""><figcaption></figcaption></figure>

I can then create a directory as a file store.

<figure><img src="../../.gitbook/assets/image (3) (1).png" alt=""><figcaption></figcaption></figure>

If I examine the directory, it allows me to create a range of file types.

<figure><img src="../../.gitbook/assets/image (4) (1).png" alt=""><figcaption></figcaption></figure>

If I examine /etc/pve/storage.cfg

```
dir: local
        path /var/lib/vz
        content vztmpl,iso,backup

lvmthin: local-lvm
        thinpool data
        vgname pve
        content images,rootdir

dir: ISOs
        path /mnt/pve/ISOs
        content backup,rootdir,iso,images,vztmpl,snippets
        is_mountpoint 1
        nodes proxmox2

```

If I only want this for ISOs, I can edit the content line.
