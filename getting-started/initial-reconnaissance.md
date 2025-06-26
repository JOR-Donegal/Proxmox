# Recce

Before I begin, I need to verify my VMWare network environment.&#x20;

<figure><img src="../.gitbook/assets/Screenshot 2025-06-26 101502.png" alt=""><figcaption></figcaption></figure>

I look at advanced settings in NAT and Host-only networks, and I also check the external network interface for the bridged connection. I derive the following table.

<table><thead><tr><th width="124">Network</th><th>Subnet</th><th>Gateway</th><th>Host</th><th>DHCP</th></tr></thead><tbody><tr><td>NAT</td><td>192.168.171.0/24</td><td>192.168.171.2</td><td>192.168.171.1</td><td>128-254</td></tr><tr><td>Host-only</td><td>192.168.209.0/24</td><td></td><td>192.168.209.1</td><td>128-254</td></tr><tr><td>Bridge</td><td>192.168.5.0/24</td><td>192.168.5.20</td><td>192.168.5.117</td><td>Any</td></tr></tbody></table>

You MUST do a recce of this type before working on any system.
