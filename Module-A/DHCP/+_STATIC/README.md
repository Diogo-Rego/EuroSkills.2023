# DHCP + STATIC

### Step 1: Identify the MAC Address of the Device

- On the device for which you want to assign a static IP, find the MAC address. The method to find the MAC address varies depending on the operating system. You can usually find it in the network settings or by running ``ipconfig`` (Windows) or ``ifconfig`` (Linux/macOS) in the command prompt or terminal.

### Step 2: Configure DHCP Reservation

- Open the DHCP server configuration file using a text editor:

```
sudo nano /etc/dhcp/dhcpd.conf
```

- Add a DHCP reservation entry for the device at the end of the configuration file. Replace the MAC address (``XX:XX:XX:XX:XX:XX``) and IP address (``192.168.1.10``) with the appropriate values:

```
host mydevice {
    hardware ethernet XX:XX:XX:XX:XX:XX;
    fixed-address 192.168.1.10;
}
```

- Save the file and exit the text editor.

### Step 3: Restart the DHCP Server

```
sudo systemctl restart isc-dhcp-server
```

- Now, the device with the specified MAC address will always receive the same IP address (192.168.1.10 in this example) from the DHCP server.