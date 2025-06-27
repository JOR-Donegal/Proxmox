# Prepare

I'm going to create virtual interfaces now in VMWare so I can configure the network in an optimal manner.&#x20;

On a bare metal host, I will need six interfaces in total.

* 2 for Management
* 2 for tagged/trunked connections for VMs
* 2 for storage

I shut down the Proxmox instance and add only one interface for each.&#x20;

On either a real server or in this virtual environment, you need to document the network interfaces in detail.

This table summarizes my VMWare configuration.

<table><thead><tr><th width="166">VMWare Adapter</th><th width="259">MAC Address</th><th width="357">Subnet</th></tr></thead><tbody><tr><td>1</td><td>00:0C:29:6D:3C:FE</td><td>NAT</td></tr><tr><td>2</td><td>00:0C:29:6D:3C:08</td><td>NAT</td></tr><tr><td>3</td><td>00:50:56:31:CA:AF</td><td>Lan Segment - Tagged</td></tr><tr><td>4</td><td>00:50:56:2E:12:9C</td><td>Lan Segment - Tagged</td></tr><tr><td>5</td><td>00:50:56:3B:E3:E0</td><td>Lan Segment - Storage</td></tr><tr><td>6</td><td>00:50:56:3E:42:DE</td><td>Lan Segment - Storage</td></tr></tbody></table>



Now I restart Proxmox to finalize my recce.&#x20;

<figure><img src="../../.gitbook/assets/Screenshot 2025-06-26 121704.png" alt=""><figcaption></figcaption></figure>

From the command line, I can map device names to MAC addresses.&#x20;

<figure><img src="../../.gitbook/assets/Screenshot 2025-06-26 121851.png" alt=""><figcaption></figcaption></figure>

My final table becomes

<table><thead><tr><th width="133">VMWare Adapter</th><th width="179">MAC Address</th><th width="288">Subnet</th><th>Linux Device</th></tr></thead><tbody><tr><td>1</td><td>00:0C:29:6D:3C:FE</td><td>NAT</td><td>ens33</td></tr><tr><td>2</td><td>00:0C:29:6D:3C:08</td><td>NAT</td><td>ens37</td></tr><tr><td>3</td><td>00:50:56:31:CA:AF</td><td>Lan Segment - Tagged</td><td>ens38</td></tr><tr><td>4</td><td>00:50:56:2E:12:9C</td><td>Lan Segment - Tagged</td><td>ens39</td></tr><tr><td>5</td><td>00:50:56:3B:E3:E0</td><td>Lan Segment - Storage</td><td>ens40</td></tr><tr><td>6</td><td>00:50:56:3E:42:DE</td><td>Lan Segment - Storage</td><td>ens41</td></tr></tbody></table>

