<p align="center">
  <a href="https://github.com/Diogo-Rego/EuroSkills.2023/tree/main/Module-A/NETWORK%20INTERFACES#network-interfaces---ipv4">
    <img src="../img/wired-network.png" alt="NETWORK INTERFACES - IPV4" width="160" height="160">
  </a>
  <h1 align="center">NETWORK INTERFACES - IPV4</h1>
</p>

### Step 1: Identify Network Interfaces

- Determine the network interface names using the ip command or by checking the ``/etc/network/interfaces`` file. Common interface names are ``eth0`` for Ethernet and ``wlan0`` for wireless.

### Step 2: Edit Network Configuration File

- Open the network configuration file using a text editor:

```
sudo nano /etc/network/interfaces
```

### Step 3: Configure Network Interfaces

- Modify the file to define the network configuration for each interface. Here's an example configuration for a typical Ethernet interface (``eth0``):

```
# The loopback network interface
auto lo
iface lo inet loopback

# The primary network interface
auto eth0
iface eth0 inet static
    address 192.168.1.100   # Replace with your desired IP address
    netmask 255.255.255.0   # Replace with your subnet mask
    gateway 192.168.1.1     # Replace with your gateway IP address
    dns-nameservers 8.8.8.8 8.8.4.4   # Replace with your DNS servers
    dns-search example.com            # Replace with your name DNS servers
```

- If you are using DHCP to obtain IP address configuration automatically, you can use the following configuration instead:

```
auto eth0
iface eth0 inet dhcp
```

- Adjust the configuration based on your network requirements, including IP address, subnet mask, gateway, and DNS servers.

### Step 4: Save the file and exit the text editor.

### Step 5: Restart Networking Service

- Restart the networking service to apply the changes:

```
sudo systemctl restart networking
```

### Step 6: Verify Network Configuration

- Use the ``ip`` command or other network tools (``ifconfig``, ``ping``, etc.) to verify that the network interface is configured correctly and functioning as expected.