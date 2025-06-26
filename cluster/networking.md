# Networking

We always have a management interface, ideally two, feeding vmbr0.

I use the second 1G interface for cluster inter-connectivity. Throughput is not important, but it needs to be low latency.

One of my 10G interfaces connects to vmbr1 to tagged traffic to VMs.

One of my 10G interfaces is dedicated for storage.

