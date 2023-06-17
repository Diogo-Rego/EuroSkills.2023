apt-get install bind9 

cd /etc/bind

nano named.conf.options	

forwarders {
    8.8.8.8;
};
dnssec-validation no;


nano named.conf.local


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