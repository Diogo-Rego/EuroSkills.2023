# ANSIBLE

Install ansible to allow you to run the playbooks
```
apt install ansible 
```
Create a directory to store all of you ansible scripts

```
mkdir /ansible
```

All the playbooks will be run in order using the command `ansible-playbook playbook.yml`
<br>

The [1-hostname](1-hostname.yml) script consists of changing the hostname of the machine based on a variable in the hosts files located in `/etc/ansible/hosts/` 
<br>

The [3a-backend](3a-backend.yml) script simple make a webserver and then change the index.html to identify with machine that site belongs 
<br>

The [3b-backend](3b-backend.yml) script makes a ftp server with tls and only the user webmaste can access it 
<br>

the [4-frontend](4-frontend.yml) script makes a HAproxy (high availability proxy) using HAproxy and keepalived for the VRRP 
