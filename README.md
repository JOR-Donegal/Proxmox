# Installation

These notes assume basic skills and understanding in Networking, Linux and Storage. If you have not covered these modules with me, talk to your lecturer before you begin.

I am going to build this as a VM under VMWare Workstation, just for testing. I make sure to enable nested virtualization. If you are installing on bare metal, the process will be the same, just without the VMWare activities.

<figure><img src=".gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

I used Debian 12 as VM type.

## Download

Go to ProxMox.com and download Proxmox VE.

<figure><img src=".gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

If you are installing on bare metal, burn this ISO on to a USB key using RUFUS or similar tool.

## Install

I use the graphical installation. Select and press return to start.

<figure><img src=".gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

I accept the end user agreement and the target hard disk.

<figure><img src=".gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

I identify the country, time zone, keyboard.

<figure><img src=".gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>

I enter a strong password and e-mail address.

<figure><img src=".gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>

I am using a NAT'd subnet in VMWare Workstation, so the defaults are fine for now.

<figure><img src=".gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>

Ready to install!

<figure><img src=".gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>

After I press **Install**, it takes a few minutes.
