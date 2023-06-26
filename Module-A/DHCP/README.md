# DHCP

### Step 1: Install the DHCP Server

```
sudo apt-get update
sudo apt-get install isc-dhcp-server
```

### Step 2: Configure the DHCP Server

- Open the DHCP server configuration file using a text editor:

```
sudo nano /etc/dhcp/dhcpd.conf
```

- Modify the configuration file according to your network settings. Here's an example configuration:

```
# Set the domain name
option domain-name "yourdomain.com";
# Set the DNS servers
option domain-name-servers 8.8.8.8, 8.8.4.4;

# Set the default lease time
default-lease-time 600;
# Set the maximum lease time
max-lease-time 7200;

# Configure the DHCP subnet
subnet 192.168.1.0 netmask 255.255.255.0 {
    range 192.168.1.100 192.168.1.200;  # Define the IP range for dynamic assignment
    option routers 192.168.1.1;  # Set the default gateway
}
```

- Customize the configuration according to your network requirements, including the domain name, DNS servers, lease times, subnet, IP range, and gateway.

- Save the file and exit the text editor.

### Step 3: Restart the DHCP Server

```
sudo systemctl restart isc-dhcp-server
```

### Step 4: Verify DHCP Server Operation

```
sudo journalctl -u isc-dhcp-server
```

- Verify that the DHCP server is providing IP addresses to clients by testing on a client device connected to the network.