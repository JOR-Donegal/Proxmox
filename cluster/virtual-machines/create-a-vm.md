# Create a VM

In the top right, click to create a VM

<figure><img src="../../.gitbook/assets/Screenshot 2025-06-29 112208.png" alt=""><figcaption></figcaption></figure>

The unique identifiers for the VMs are cluster wide. It does make keeping track of VMs a little easier.

<figure><img src="../../.gitbook/assets/Screenshot 2025-06-29 112457.png" alt=""><figcaption></figcaption></figure>

Click **Next**.

Now I select the ISO image to use and click **Next**.

<figure><img src="../../.gitbook/assets/Screenshot 2025-06-29 112638.png" alt=""><figcaption></figcaption></figure>

I leave the System tab at defaults and proceed to Disks. For storage, I select my pool, JOR1. I used a small disk size (4GB) and set write back caching, but have had some problems with this. My installs are more stable when I use a 32GB disk size.

<figure><img src="../../.gitbook/assets/Screenshot 2025-06-29 113125.png" alt=""><figcaption></figcaption></figure>

I use defaults for CPU and memory.

I leave default network settings and on the Confirm screen, I click Finish.

I start the VM and go through a conventional Ubuntu Server installation, picking the minimums for everything.

When I finish, I remove the ISO file from the image. This is a local resource, you cannot move a VM between servers if its constrained by a resource local to a single server.&#x20;

<figure><img src="../../.gitbook/assets/Screenshot 2025-06-29 131039.png" alt=""><figcaption></figcaption></figure>
