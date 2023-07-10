# DDNS


named.conf.local
```
key DHCP_UPDATER {
    algorithm HMAC-MD5.SIG-ALG.REG.INT;
    secret pRP5FapFoJ95JEL06sv4PQ==;
}

zone "localhost" {
    type master;
    file "/var/cache/bind/db.localhost.com";
    allow-update { DHCP_UPDATER; };
};

zone "x.x.x.in-addr.arpa" {
    type master;
    file "/var/cache/bind/db.x.x.x";
    allow-update { DHCP_UPDATER; };
};
```
named.conf.option 

```
options {
        forwarders{
                8.8.8.8;
        };
        dnssec-validation no;
        auth-nxdomain no; 
        allow-recursion { any; };
        listen-on-v6 { any; };
}
```