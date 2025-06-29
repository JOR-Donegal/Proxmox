# Installation

The tool for installation in Ceph is called **pveceph.** It more more precise and repeatable to work from the CLI. To see the scope of the **pveceph** command, type

```
pveceph help
```

We need to install Ceph on _each_ server in the cluster, for example

```
root@pve31:~# pveceph install --repository no-subscription
```

##
