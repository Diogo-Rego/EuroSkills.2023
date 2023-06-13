# IPTables

## Rules

**bloquear tudo**
iptables –P INPUT DROP
iptables –P OUTPUT DROP
iptables –P FORWARD DROP

**Para conseguir ter acesso a si mesmo**
iptables –A INPUT –i lo –j ACCEPT
iptables –A OUTPUT –o lo –j ACCEPT

**Permitir ICMP**
iptables -A INPUT -p icmp  -j ACCEPT
iptables -A OUTPUT -p icmp -j ACCEPT
iptables -A FORWARD -p icmp -j ACCEPT

**Permitir Regra Individual**
iptables –A INPUT -i * –p tcp –-dport * -m state --state NEW,RELATED,ESTABLISHED -j ACCEPT
iptables –A OUTPUT -o * –p tcp –-sport * –m state --state RELATED,ESTABLISHED –j ACCEPT

iptables –A FORWARD -i * –p tcp –-dport * -m state --state NEW,RELATED,ESTABLISHED -j ACCEPT
iptables –A FORWARD -o * –p tcp –-sport * –m state --state RELATED,ESTABLISHED –j ACCEPT
iptables –A FORWARD -i * –p tcp –-dport * -m state --state RELATED,ESTABLISHED -j ACCEPT
iptables –A FORWARD -o * –p tcp –-sport * –m state --state NEW,RELATED,ESTABLISHED –j ACCEPT


**Permitir Regras de Múltiplas Portas**
iptables -A INPUT -p tcp/udp -i interface -m  multiport --dport X,X,X,X,X  -m state --state NEW,RELATED,ESTABLISHED -j ACCEPT
iptables -A OUTPUT -p tcp/udp -o interface -m  multiport --sport X,X,X,X,X -m state --state RELATED,ESTABLISHED -j ACCEPT

iptables -A FORWARD -p tcp/udp -i interface -m  multiport --dport X,X,X,X,X  -m state --state NEW,RELATED,ESTABLISHED -j ACCEPT
iptables -A FORWARD -p tcp/udp -o interface -m  multiport --sport X,X,X,X,X -m state --state RELATED,ESTABLISHED -j ACCEPT
iptables -A FORWARD -p tcp/udp -i interface -m  multiport --dport X,X,X,X,X  -m state --state RELATED,ESTABLISHED -j ACCEPT
iptables -A FORWARD -p tcp/udp -o interface -m  multiport --sport X,X,X,X,X -m state --state NEW,RELATED,ESTABLISHED -j ACCEPT

**NAT/PAT - OUTSIDE**
iptables -t nat -A POSTROUTING -o interface -j MASCARADE 

**NAT - INSIDE - PORT FORWADING - Múltiplas Portas**
iptables -t nat -A PREROUTING -i interface -p tcp/udp -m multiport --dport X,X,X,X -j DNAT --to-destination X.X.X.X  

**NAT - INSIDE - PORT FORWADING - Portas Individuais**
iptables -t nat -A PREROUTING -i interface -p tcp/udp --dport X -j DNAT --to-destination X.X.X.X

**NAT - INSIDE - PORT FORWADING - Encaminhar todo o tráfico**
iptables -t nat -A PREROUTING -i interface -j DNAT --to-destination X.X.X.X

apt-get install netfilter-persistent iptables-persistent

netfilter-persistent flush - limpa a memória e coloca todas as tables [filter, net, raw, mangle, security] em ACCEPT 
netfilter-persistent reload - copia de /etc/iptables/rules.v4 para a memória
netfilter-persistent save  - Uso este comando para guardar em /etc/iptables/rules.v4 as regras da firewall que estão em memória

**Criar Falso Servidor de Echo - TCP**
socat -v tcp-l:1234,fork exec:'/bin/cat' &
**Criar Falso Servidor de Echo - TCP**
socat -v udp-l:1234,fork exec:'/bin/cat' &

**Testar Portas de Servidor - TCP**
netcat -u host port
**Testar Portas de Servidor - UDP**
netcat -u host port

cd /proc 
find . | grep vlan
ipv4.conf.ens33.proxy_arp_pvlan=1
