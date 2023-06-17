## DHCP failover
Install the DHCP server
```
apt-get install isc-dhcp-server
```
missing the config to indicate with interface to deal the ip addresses

DHCP configuration folder
```
cd /etc/dhcp
```
DHCP configuration file
```
nano dhcpd.conf
```
DHCP configuration

```
option domain-name "Firmatpolska.pl"; 
option domain-name-servers 192.168.30.254 ;
authoritative;
subnet 192.168.30.0 netmask 255.255.255.0 {~
    failover peer "failover" {
        primary;
        address 192.168.10.1; 
        peer address 192.168.10.2; 
        mclt 1800;
        split 128;
    }
    option routers 192.168.30.254;
    option domain-name "firmatpolska.pl";
    option domain-name-servers 192.168.30.254;
    pool {
        range 192.168.30.1 192.168.30.253;
        failover peer "failover";
    }
}
```

If you need to config a static ip with DHCP
```
host *hostname {
    hardware ethernet X:X:X:X:X:X; # MAC ADDRESS
    fixed-address X.X.X.X 
}
```

Restart DHCP server
```
systemctl enable isc-dhcp-server
systemctl restart isc-dhcp-server
```