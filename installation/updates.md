# Updates

If I try to do updates, it will fail, as I do not have an enterprise license. We can change this by selecting Repositories,  Add, and then in the drop down box, select No-Subscription.&#x20;

<figure><img src="../.gitbook/assets/image (19).png" alt=""><figcaption></figcaption></figure>

I disable the two enterprise repositories (click on them and then click **disable**).

<figure><img src="../.gitbook/assets/image (20).png" alt=""><figcaption></figcaption></figure>

&#x20;I go back to updates and click refresh.&#x20;

<figure><img src="../.gitbook/assets/image (21).png" alt=""><figcaption></figcaption></figure>

I click Upgrade and a console window opens to perform this.

<figure><img src="../.gitbook/assets/image (22).png" alt=""><figcaption></figcaption></figure>

Always best to do a reboot if you can.

If I change to the terminal, I can see where my repo source are.

```
cd /etc/apt/sources.list.d/
ls -l
```

Examine these files. The enterprise repos should be commented out.

If you navigate to **/etc/apt**, you can can check the **sources.list** file to see what repos you are using.

After confirming this, you could also do future updates via the command prompt using

```
apt update
apt upgrade
```

