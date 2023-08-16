Install Free Range Routing (FRR)
```
apt install frr 
```
go to the frr directory 
```
cd /etc/frr/
```
enable ospf
```
nano daemons
```
change the line below form no to yes 
```
ospfd=yes
```
copy the example to the config folder 
```
cp /usr/share/doc/frr/examples/ospfd.conf.sample .
```
change the config name 
```
cp ospfd.conf.sample ospfd.conf
```
edit the config normally only need to change the network 
```
nano ospfd.conf
                                 
    ! -*- ospf -*-
    !
    ! OSPFd sample configuration file
    !
    !
    hostname ospfd
    password zebra
    !enable password please-set-at-here
    !
    router ospf
      network 10.20.23.0/25 area 0
      network 10.20.23.128/25 area 0
    !
    log stdout
```
change the owner and permissions of the file 
```
chown frr:frr ospfd.conf
chmod 640 ospfd.conf 
```
