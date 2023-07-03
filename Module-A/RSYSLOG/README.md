# RSYSLOG

Set up the rsyslog server:

````
nano /etc/rsyslog.conf
````

````
# provides UDP syslog reception
module(load="imudp")
input(type="imudp" port="514")
````

````
nano /etc/rsyslog.d/50-default.conf
````

````
if $hostname == 'SRV' then /var/log/SRV.log
if $username == 'ubuntu' then /var/log/ubuntu.log
if $programname == 'dhcp' then /var/log/dhcp.log
````

### Client

````
nano /etc/rsyslog.conf
````

````
*.* @server_ip_address:514
````

Replace ``server_ip_address`` with the IP address or hostname of the rsyslog server. The ``@`` symbol specifies the use of UDP for log forwarding. If you prefer TCP, use ``@@`` instead.

- Restart rsyslog service: Save the file and restart the rsyslog service on the client machine(s) to apply the configuration changes. Again, the command to restart the service depends on the Linux distribution. On Ubuntu, you can use:

````
sudo service rsyslog restart
````
