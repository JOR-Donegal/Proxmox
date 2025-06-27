# Updates

If I try to do updates, it will fail, as I do not have an enterprise license. Review [here](https://pve.proxmox.com/wiki/Package_Repositories).

In the left pane, select the server.

We can change this by selecting **Repositories**, **Add,** and then in the drop down box, select **No-Subscription**.

<figure><img src="../../.gitbook/assets/image (13).png" alt=""><figcaption></figcaption></figure>

I disable the two enterprise repositories (click on them and then click **disable**).

<figure><img src="../../.gitbook/assets/image (14).png" alt=""><figcaption></figcaption></figure>

I go back to updates and click refresh.

<figure><img src="../../.gitbook/assets/image (15).png" alt=""><figcaption></figcaption></figure>

I click Upgrade and a console window opens to perform this.

<figure><img src="../../.gitbook/assets/image (16).png" alt=""><figcaption></figcaption></figure>

Always best to do a reboot if you can.

If I change to the terminal, I can see where my repo source are.

```
cd /etc/apt/sources.list.d/
ls -l
```

Examine these files. The enterprise repos should be commented out.

If you navigate to **/etc/apt**, you can can check the **sources.list** file to see what repos you are using.

```
deb http://ftp.ie.debian.org/debian bookworm main contrib
deb http://ftp.ie.debian.org/debian bookworm-updates main contrib
# security updates
deb http://security.debian.org bookworm-security main contrib
deb http://download.proxmox.com/debian/pve bookworm pve-no-subscription
```

After confirming this, you could also do future updates via the command prompt using

```
apt update
apt upgrade
```
