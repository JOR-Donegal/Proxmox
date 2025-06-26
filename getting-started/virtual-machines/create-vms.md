# Create VMs

I have uploaded an ISO, in this sequence I will create a first VM. Click on the button in the top right corner.

<figure><img src="../../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

I still have only one node called **pve21**.

<figure><img src="../../.gitbook/assets/Screenshot 2025-06-26 111535.png" alt=""><figcaption></figcaption></figure>

I will name my VM as **ub2204-server**, this is my code for a gold image. Then I click **next**.

<figure><img src="../../.gitbook/assets/Screenshot 2025-06-26 113546.png" alt=""><figcaption></figcaption></figure>

I select **local** as my storage and I select the ISO file I uploaded previously. Then I click **next**.

<figure><img src="../../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

Under **System** I leave the defaults, but enable **Qemu agent**, to allow the VM to communicate with the Host.

Under **Disks**, I leave the defaults.

<figure><img src="../../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

Under **CPU** and **Memory**, I leave the defaults.

<figure><img src="../../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

Under **Network**, I leave the default. This will connect the VM to the same bridge as the management interface. OK for the test!

<figure><img src="../../.gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>

Finally, I record all my settings.

<figure><img src="../../.gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>

I have ticked **Start after created**. I click **Finish**.

I can see the VM has been created.

<figure><img src="../../.gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>

And now I can start it and install the guest OS.

<figure><img src="../../.gitbook/assets/image (20).png" alt=""><figcaption></figcaption></figure>

I am not going to document the install, I presume you know how to do this! However, its best to install minimums of everything.
