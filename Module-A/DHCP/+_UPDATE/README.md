<p align="center">
  <h1 align="center">DHCP + UPDATE</h1>
</p>

- Then add the zones for the dynameic dns.

  - Key provaided from the dhcpd.conf documentation for the ddns.

````
key DHCP_UPDATER {
    algorithm HMAC-MD5.SIG-ALG.REG.INT;
    secret pRP5FapFoJ95JEL06sv4PQ==;
}
````

- Zones configuration

````
zone fimatpolska.pl. {
    primary 192.168.10.254;  #DNS server 
    key DHCP_UPDATER;            
}

zone 0.168.192.in-addr.arpa. {
primary 192.168.10.254;
key DHCP_UPDATER;
}

zone 15.168.192.in-addr.arpa. {
primary 192.168.10.254;
key DHCP_UPDATER;
}

zone 0.16.172.in-addr.arpa. {
primary 192.168.10.254;
key DHCP_UPDATER;
}
````