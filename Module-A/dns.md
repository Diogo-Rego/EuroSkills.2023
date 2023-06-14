


nano named.conf.options
```
forwarders {
  8.8.8.8;
};
```

nano named.conf.local
```
zone "pdl.pl" {
        type master;
        file "/var/lib/bind/db.pdl.pl";
};

zone "31.168.192.in-addr.arpa" {
        type master;
        file "/var/lib/bind/db.31.168.192";
};
```

```
```

```
```

```
```

```
-A INPUT -p tcp -m tcp -m multiport --dports 22,80,443,2222,3389 -m state --state NEW,RELATED,ESTABLISHED -j ACCEPT
-A INPUT -p icmp -m icmp --icmp-type 0 -m state --state RELATED,ESTABLISHED -j ACCEPT
-A INPUT -s 172.31.0.0/30 -p icmp -m icmp --icmp-type 8 -m state --state NEW,RELATED,ESTABLISHED -j ACCEPT
-A INPUT -i ens224 -p icmp -m icmp --icmp-type 8 -m state --state NEW,RELATED,ESTABLISHED -j ACCEPT
-A INPUT -p tcp -m tcp -m state --state RELATED,ESTABLISHED -j ACCEPT
-A INPUT -p udp -m udp -m state --state RELATED,ESTABLISHED -j ACCEPT
-A INPUT -m limit --limit 30/min -j LOG --log-prefix "IPT:INP:Denied: " --log-level 7
-A INPUT -j REJECT --reject-with icmp-port-unreachable
-A INPUT -p icmp -j ACCEPT
-A FORWARD -i ens224 -o ens256 -p tcp -m tcp -m multiport --dports 20,21,22,80,443 -m state --state NEW,RELATED,ESTABLISHED -j ACCEPT
-A FORWARD -i ens256 -o ens224 -p tcp -m tcp -m multiport --sports 20,21,22,80,443 -m state --state RELATED,ESTABLISHED -j ACCEPT
-A FORWARD -i ens224 -o ens256 -p icmp -m icmp --icmp-type 8 -m state --state NEW,RELATED,ESTABLISHED -j ACCEPT
-A FORWARD -i ens256 -o ens224 -p icmp -m icmp --icmp-type 0 -m state --state RELATED,ESTABLISHED -j ACCEPT
-A FORWARD -i ens224 -o ens192 -p tcp -m tcp -m multiport --dports 20,21,22,80,443 -m state --state NEW,RELATED,ESTABLISHED -j ACCEPT
-A FORWARD -i ens192 -o ens224 -p tcp -m tcp -m multiport --sports 20,21,22,80,443 -m state --state RELATED,ESTABLISHED -j ACCEPT
-A FORWARD -i ens224 -o ens192 -p icmp -m icmp --icmp-type 8 -m state --state NEW,RELATED,ESTABLISHED -j ACCEPT
-A FORWARD -i ens192 -o ens224 -p icmp -m icmp --icmp-type 0 -m state --state RELATED,ESTABLISHED -j ACCEPT
-A FORWARD -i ens224 -o ens192 -p udp -m udp --dport 53 -m state --state NEW,RELATED,ESTABLISHED -j ACCEPT
-A FORWARD -i ens192 -o ens224 -p udp -m udp --sport 53 -m state --state RELATED,ESTABLISHED -j ACCEPT
-A FORWARD -m limit --limit 30/min -j LOG --log-prefix "IPT:FWD:Denied: " --log-level 7
-A FORWARD -j REJECT --reject-with icmp-port-unreachable
-A OUTPUT -p tcp -m tcp -m state --state NEW,RELATED,ESTABLISHED -j ACCEPT
-A OUTPUT -p udp -m udp -m state --state NEW,RELATED,ESTABLISHED -j ACCEPT
-A OUTPUT -m limit --limit 30/min -j LOG --log-prefix "OUT:INP:Denied: " --log-level 7
-A OUTPUT -j REJECT --reject-with icmp-port-unreachable
```
