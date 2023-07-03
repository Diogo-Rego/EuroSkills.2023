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
8.8.8.8
};
dnssec-validation no;
auth-nxdomain no;
allow-recursion { any; }
listen-on-v6 { any; };
```
Set the zones you want 
```
nano named.conf.local
```
Zones Configuration 
```
# missing the key for the DHCP_UPDATER 


zone "firmatpolska.pl." {
    type master;
    file "/etc/bind/db.firmatpolska.pl";
    allow-update {key <the key for the dhcp updater> } 
};

zone "10.168.192.in-addr.arpa." { 
    type master;
    file "/etc/bind/db.192.168.10";
    allow-update {key <the key for the dhcp updater> } 
};

zone "20.168.192.in-addr.arpa." {
    type master;
    file "/etc/bind/db.192.168.20";
    allow-update {key <the key for the dhcp updater> } 
};

zone "30.168.192.in-addr.arpa." {
    type master;
    file "/etc/bind/db.192.168.30";
    allow-update {key <the key for the dhcp updater> } 
};
```

## WEB server

Install the WEB server  
```
apt install apache2 
```
enable the ssl for the https 
```
a2enmod ssl 
```
enable the ssl site 
```
a2ensite default-ssl.conf 
```
folder where you can find the sites that are active 
```
cd /etc/apache/sites-avalible
```
config the ssl site to change the certs 
```
nano default-ssl.conf 
```
after the configutation is done restart apache2 
```
systemctl restart apache2 
```

## EMAIL server 

sudo apt install postfix dovecot-imapd dovecot-pop3d 




