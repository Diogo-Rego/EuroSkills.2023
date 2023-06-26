# DHCP RELAY

````
apt install isc-dhcp-relay
````

````
dpkg-reconfigure isc-dhcp-relay
````

````
nano /etc/default/isc-dhcp-relay
````

````
# What servers should the DHCP relay forward requests to?
SERVERS="192.168.10.1 192.168.10.2"

# On what interfaces should the DHCP relay (dhrelay) serve DHCP requests?
INTERFACES="ens161"
````