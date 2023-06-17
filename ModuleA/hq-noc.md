DHCP failover 

apt-get install isc-dhcp-server

cd /etc/dhcp

nano dhcpd.conf

```
option domain-name "Firmatpolska.pl"; 
option domain-name-servers 192.168.10.254 ;
authoritative;
subnet 192.168.30.0 netmask 255.255.255.0 {~
    failover peer "failover" {
        secondary;
        address 192.168.10.2; 
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