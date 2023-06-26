# DHCP + FAILOVER

### Step 1: Configure Primary DHCP Server

- Edit the DHCP server configuration file on the primary node:

```
sudo nano /etc/dhcp/dhcpd.conf
```

- Configure the DHCP server options and define the DHCP subnet as per your network requirements.

- Add the following lines at the end of the configuration file to enable failover:

```
failover peer "dhcp-failover" {
    primary;  # Set as primary on this node
    address <Primary-IP>;  # Replace with the IP address of this node
    port 647;  # Use a unique port for failover communication
    peer address <Secondary-IP>;  # Replace with the IP address of the secondary node
    peer port 647;  # Use the same port as configured on the secondary node
    max-response-delay 30;  # Maximum delay in seconds for receiving an acknowledgment from the peer
    max-unacked-updates 10;  # Maximum number of unacknowledged updates
    load balance max seconds 3;  # Maximum load balance interval
    mclt 1800;  # Maximum client lead time
    split 128;  # Percentage split for load balancing
}
```

- Save the file and exit the text editor.

### Step 2: Configure Secondary DHCP Server

- Edit the DHCP server configuration file on the secondary node:

```
sudo nano /etc/dhcp/dhcpd.conf
```

- Configure the DHCP server options and define the DHCP subnet as per your network requirements.

- Add the following lines at the end of the configuration file to enable failover:

```
failover peer "dhcp-failover" {
    secondary;  # Set as secondary on this node
    address <Secondary-IP>;  # Replace with the IP address of this node
    port 647;  # Use the same port as configured on the primary node
    peer address <Primary-IP>;  # Replace with the IP address of the primary node
    peer port 647;  # Use the same port as configured on the primary node
    max-response-delay 30;  # Maximum delay in seconds for receiving an acknowledgment from the peer
    max-unacked-updates 10;  # Maximum number of unacknowledged updates
    load balance max seconds 3;  # Maximum load balance interval
    mclt 1800;  # Maximum client lead time
    split 128;  # Percentage split for load balancing
}
```

- Save the file and exit the text editor.

### Step 3: Restart DHCP Servers

- Restart the DHCP servers on both nodes to apply the changes:

```
sudo systemctl restart isc-dhcp-server
```

### Step 4: Verify Failover Status

- Check the failover status using the following command on both nodes:

```
sudo dhcpd -t -cf /etc/dhcp/dhcpd.conf
```

- Now, your DHCP servers are configured as a failover cluster, ensuring high availability and redundancy. The primary node will handle most of the DHCP requests, and the secondary node will take over if the primary node becomes unavailable. Make sure to replace ``<Primary-IP>``, ``<Secondary-IP>``, and ``<Netmask>`` with the appropriate values for your network configuration.c