firts nat 

apt install iptabls iptables-persistent netfilter-persistent 

nano /etc/sysctl.conf 


uncomment ipv4 forwarding 

then enable nat 


iptables -t nat -A POSTROUTING -o ens<interface-internet-facing> -j MASQUERADE
iptables -t nat -A PREROUTING -t udp --dport 53 -j DNAT --to-destination <socket from dmz> #DNS
iptables -t nat -A PREROUTING -t tcp --dport 25 -j DNAT --to-destination <socket from dmz> #SMTP
iptables -t nat -A PREROUTING -t tcp --dport 143 -j DNAT --to-destination <socket from dmz> #IMAP
iptables -t nat -A PREROUTING -t tcp --dport 110 -j DNAT --to-destination <socket from dmz> #POP3
iptables -t nat -A PREROUTING -t tcp --dport 80 -j DNAT --to-destination <socket from dmz> #HTTP
iptables -t nat -A PREROUTING -t tcp --dport 443 -j DNAT --to-destination <socket from dmz> #HTTPS

apt install easy-rsa 

cp /usr/share/easy-rsa /etc/ 

cd /etc/easy-rsa  

cp vars.example vars 

nano vars 

change what you need to make the certificate 

./easy-rsa init-pki 

./easy-rsa build-ca nopass 

./easy-rsa --subject-alt-name=DNS:www.firmatpolska.pl gen-rq www.fitmatpolska.pl
./easy-rsa sign-rq server www.fitmatpolska.pl
./easy-rsa --subject-alt-name=DNS:internal.firmatpolska.pl gen-rq internal.fitmatpolska.pl
./easy-rsa sign-rq server internal.fitmatpolska.pl
./easy-rsa --subject-alt-name=DNS:firmatpolska.pl gen-rq mail.fitmatpolska.pl
./easy-rsa sign-rq server mail.fitmatpolska.pl 


apt install openvpn 

copy examples of openvpn to /etc/openvpn/

then make a site to site vpc with the datacenter and a remote desktop with a external host 

