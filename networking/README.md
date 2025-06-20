# Networking

I assume you have a background in networking, if not, discuss with your lecturer before proceeding. On any virtualization server, I will probably have four or more interfaces connecting to two separate Top of Rack switches (ToR). I may have two separate interfaces connecting to two back-end switches (BE) for a storage network if I'm using one. In some cases, this is all collapsed into two high-speed interfaces and trunking is used to provide the required range of functionality.&#x20;

* Management - 2 x 10Gb/s interface to two different ToR switches, may also be used for live migration etc.
* Tagged/Trunk - 2 x 10Gb/s or faster interfaces to two different ToR switches, used by VMs.
* Storage - depends on the architecture, 2 x 10Gb/s or faster interfaces to two different BE switches for iSCSI, 2 x FC interfaces for fiber channel, etc.
* BMC - most servers will have a baseboard management controller (BMC). In Dell equipment, this is iDRAC, in HP, this is the ILO. This will normally be a single interface to a dedicated management switch.

The above implies up to seven interfaces to five different switches, per rack!

Ethernet devices are named as _**en**_ and in systemd, the next letter is for devices on a board (o) or the slot (s); there are other options. My first physical interface is **ens33**.

