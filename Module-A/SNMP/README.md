# SNMP 

````
apt install snmpd
````

Edit the file:

````
/etc/snmp/snmpd.conf 
````

Set the SNMP v1 Read-Only Community String as 'public' by adding the line:

````
rocommunity public
````

#agentAddress udp is the IP address from which SNMP requests will be accepted by the server. Hence, comment the line:

````
#agentAddress udp:127.0.0.1:161
````

For the same reason mentioned above, uncomment the line: 

````
agentAddress udp:161,udp6:[::1]:161
````

Restart the snmpd service:

````
service snmpd restart
````