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









generate the key for the DHCP Updater and for the fail over
```
rndc-confgen -a -b 512 # -a to identify the algorithen and -b for the number of byter 
```
after generating a key copy and paste the key on dhchp.conf and named.conf.local 

example of the key generated :

```
key "ddns-key" {
algorithm hmac-sha256;
secret "zDQMycm2qO5ERDdGvhMWtjAWAPd6ZxCG0LE1YOsESW+ZRj9pjR+n2hZ/bqYe2dGh8XdQ+TrMKcKfb18JGOHD2g==";
}
```

```
failover peer "failover" {
    primary;                      #means that is main server
    address 192.168.0.1;          #local ip
    peer address 192.168.0.2;     #ip the the secondary failover server
    port 519;                     #local port for failover
    peer port 520;                #port to use to connec
    mclt 1800;                    #Dont know yet
    split 128;                    #Dont know yet
    load balance max seconds 3;   #Dont know yet
    max-response-delay 60;        #Dont know yet
    max-unacked-updates 10;       #Dont know yet
}
```
the configuration for the subnets for the dhcp 
```
subnet 192.168.10.0 netmask 255.255.255.0 {
    option routers 192.168.10.254;
    option broadcast-address 192.168.10.255;
    pool {
        failover peer "failover";
        range 192.168.10.1 192.168.10.252;
    }
}
subnet 192.168.30.0 netmask 255.255.255.0 {
    option routers 192.168.30.254;
    option broadcast-address 192.168.30.255;
    pool {
        failover peer "failover";
        range 192.168.30.1 192.168.30.252;  
    }
}
```
if you need to config 
```
host  <hosname of the machine>{
hardware ethernet <mac address >;
fixed-address <ip or domain name>;
}
```

apt install slapd ldap-utils 

nano /etc/ldap/ldap.conf


BASE    dc=openldap-tutorial,dc=local
URI     ldap://ldap.example.com ldap://ldap-master.example.com:666

TLS_CACERT      /etc/ssl/certs/ca-certificates.crt

dpkg-reconfigure slapd

<firmatpolska.pl>
<firmatpolska>
<MDB>
<no>
<yes>


