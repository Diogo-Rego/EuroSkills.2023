<p align="center">
  <a>
    <img src="../../img/nat-gateway.png" alt="NAT" width="160" height="160">
  </a>
  <h1 align="center">NAT</h1>
</p>

### Step 1: Install iptables (if not already installed)

Most Debian installations come with iptables pre-installed. If it's not present on your system, install it using the following command:

````
sudo apt update
sudo apt install iptables
````

To make the iptables rules persistent across reboots, you can use the iptables-persistent package, which is available in Debian:

````
sudo apt install iptables-persistent
````

During the installation, it will ask you whether you want to save the current IPv4 rules. Select "Yes" to save them.

### Step 2: Enable IP forwarding

IP forwarding must be enabled for your system to act as a router and perform NAT. Open the sysctl.conf file to make this change:

````
sudo nano /etc/sysctl.conf
````

Uncomment or add the following line to enable IP forwarding:

````
net.ipv4.ip_forward=1
````

Save the file and apply the changes with:

````
sudo sysctl -p
````

### Step 3: Configure iptables port forwarding rule

Open a terminal and run the following iptables command to set up the port forwarding rule:

````
sudo iptables -t nat -A PREROUTING -i eth0 -p tcp --dport 80 -j DNAT --to 192.168.1.100:80
````

In this command:

- ``-t nat``: Specifies the NAT table in iptables.

- ``-A PREROUTING``: Appends the rule to the PREROUTING chain, which is used for altering incoming packets.

- ``-i eth0``: Specifies the network interface through which the incoming traffic arrives (replace eth0 with your actual internet-facing interface).

- ``-p tcp``: Specifies that the forwarding is for TCP traffic.

- ``--dport 80``: Specifies the destination port (port 80 for HTTP).

- ``-j DNAT``: Redirects the packet to the specified destination address.

- ``--to 192.168.1.100:80``: Specifies the local IP address (192.168.1.100) and port (80) to which the traffic will be forwarded.

### Step 4: Enable IP masquerading (if not already enabled)

IP masquerading allows the response traffic from the local server to go back through the Debian machine, which acts as a gateway.

````
sudo iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE
````

Replace ``eth0`` with your actual internet-facing interface.

### Step 5: Save iptables rules

To save the current iptables rules to be loaded on boot, use the following commands:

````
netfilter-persistent save
````

### Step 5: Reload iptables rules

````
netfilter-persistent reload
````

- IPv4 Rules: The rules for IPv4 are saved in the /etc/iptables/rules.v4 file.
- IPv6 Rules: The rules for IPv6 are saved in the /etc/iptables/rules.v6 file.

The package iptables-persistent automatically loads the rules from these two files during system startup, applying the saved rules to configure the iptables firewall.

