# Create VMs

I have uploaded an ISO, in this sequence I will create a first VM. Click on the button in the top right corner.

<figure><img src="../.gitbook/assets/image (28).png" alt=""><figcaption></figcaption></figure>

I still have only one node called **pve**.

<figure><img src="../.gitbook/assets/image (29).png" alt=""><figcaption></figcaption></figure>

I will name my VM as **ub2204-server**, this is my code for a gold image. Then I click **next**.

I select **local** as my storage and I select the ISO file I uploaded previously. Then I click **next**.&#x20;

<figure><img src="../.gitbook/assets/image (30).png" alt=""><figcaption></figcaption></figure>

Under **System** I leave the defaults, but enable **Qemu agent**, to allow the VM to communicate with the Host.

Under **Disks**, I leave the defaults.

<figure><img src="../.gitbook/assets/image (31).png" alt=""><figcaption></figcaption></figure>

Under **CPU** and **Memory**, I leave the defaults.

<figure><img src="../.gitbook/assets/image (32).png" alt=""><figcaption></figcaption></figure>

Under **Network**, I leave the default. This will connect the VM to the same bridge as the management interface. OK for the test!

<figure><img src="../.gitbook/assets/image (33).png" alt=""><figcaption></figcaption></figure>

Finally, I record all my settings.

<figure><img src="../.gitbook/assets/image (34).png" alt=""><figcaption></figcaption></figure>

I have ticked **Start after created**. I click **Finish**.

I can see the VM has been created.

<figure><img src="../.gitbook/assets/image (35).png" alt=""><figcaption></figcaption></figure>

And now I can install the guest OS.

<figure><img src="../.gitbook/assets/image (38).png" alt=""><figcaption></figcaption></figure>

I am not going to document the install, I presume you know how to do this!
