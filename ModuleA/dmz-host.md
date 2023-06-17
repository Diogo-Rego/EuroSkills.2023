## DNS 
Install Bind9 for DNS server 
```
apt-get install bind9 
```
DNS configuration folder 
```
cd /etc/bind
```
Set a Forward dns in case you don't have the name for the ip
```
nano named.conf.options	
```
```
forwarders {
    8.8.8.8;
};
dnssec-validation no;
```
Set the zones you want 
```
nano named.conf.local
```
Zones Configuration 
```
zone "firmatpolska.pl." {
    type master;
    file "/etc/bind/db.firmatpolska.pl";
};

zone "10.168.192.in-addr.arpa." { 
    type master;
    file "/etc/bind/db.192.168.10";
};

zone "20.168.192.in-addr.arpa." {
    type master;
    file "/etc/bind/db.192.168.20";
};

zone "30.168.192.in-addr.arpa." {
    type master;
    file "/etc/bind/db.192.168.30";
};
```