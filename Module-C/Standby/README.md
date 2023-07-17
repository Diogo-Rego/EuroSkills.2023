# Standby


interface Vlan12
ip address 172.20.3.254 255.255.255.0
ip helper-address 172.20.4.2
ip pim sparse-mode
standby 1 ip 172.20.3.252
standby 1 priority 120
standby 1 preempt
standby 1 authentication md5 key-string cisco

