<p align="center">
  <a>
    <img src="img/Linux_Environment.png" alt="Linux Environment" width="160" height="160">
  </a>
  <h1 align="center">Module A – Linux Environment</h1>
</p>

# INTRODUCTION

The competition has a fixed start and finish time. You must decide how to best divide your time.

**Please carefully read the following instructions!**

When the competition time ends, please leave your station in a running state. The assessment will be done in the state as it is. **No reboot will be initiated as well as powered off machines will not be powered on!**

Please use the information below for all the servers and clients.

# LOGIN

<table>
  <tr>
    <th>Username:</th>
    <td>root</td>
    <td>localadmin</td>
  </tr>
  <tr>
    <th>Password:</th>
    <td>Passw0rd!</td>
    <td>Passw0rd!</td>
  </tr>
</table>

Use the string Passw0rd! as password everywhere where a password, passphrase etc is needed.

**Pay attention to the zero sign in the string that replaces the capital O!**

# SYSTEM CONFIGURATION

<table>
  <tr>
    <th>Region/timezone:</th>
    <td>Europe/Warsaw</td>
  </tr>
  <tr>
    <th>Locale:</th>
    <td>English US (UTF-8)</td>
  </tr>
  <tr>
    <th>Key Map:</th>
    <td>English US</td>
  </tr>
</table>

# RESOURCES

> You will find the topology and the listing of used IP addresses at the end of this document. The list of the users to be created can be found there too.

# PREINSTALLED RESOURCES

> Every system in this task uses **Debian 11**. Every VM you see in the topology chart at the end of this document is preinstalled on the physical host, named accordingly. The hosts use VMware ESXi as a virtualisation platform and you can connect to the resources using your laptops with vSphere Web Client or VMware Workstation also.

**You can connect to the ESXi host with esxi.local URL.**

> The preinstalled VMs contain only the base system and few additional packages (see in the software section), you can install additional software using virtual optical disks.

# SOFTWARE

> For testing purpose, all VM has been installed with the following test tools: 

```
smbclient, curl, lynx, dnsutils, ldap-utils, ftp, lftp, wget, ssh, nfs-common, rsync, telnet, traceroute, tcptraceroute, tcpdump, net-tools, cifs-utils.
```

**You can find a Debian install ISOs in the datastore.**

# INDRUSTY COMPLIANCE

> The test project does not always give you an exact specification. In these situations you have the chance to choose which software to use, which path to follow - you will find information at the tasks about the paths you can choose from. The more sophisticated a solution is the better mark you are going to get for it.

# DESCRIPTION OF PROJECT AND TASKS

> You are a new IT Engineer of the Firma Tradycyjna Polska Sp. z o.o. company. The goal of your next project is to build the whole IT infrastructure of the company.

# General Configuration

Set up all the resources with the following:

- [hostname,](Basic_Configuration/HOSTNAME/README.md)
- [network configuration,](Basic_Configuration/NETWORK_INTERFACES/README.md)
- [time zone,](Basic_Configuration/TIMEZONE/README.md)
- [keyboard layout,](Basic_Configuration/Keyboard_Layout/README.md)
- [install SSH server and allow root password access](Basic_Configuration/SSH/README.md) (for the easiest testing).

# Corporate HQ

This is the company’s headquarters site with limited server services and clients.

### fw-hq

> This is the edge router and firewall of the HQ site. For this reason, it should allow devices to reach each other between network segments and the Internet.

You must configure the services of this server according to the following requirements.

1. **Create a root certificate authority** ([Easy-RSA](EasyRSA/README.md)). Use the next parameters:

````
C=PL, O=Firma Tradycyjna Polska Sp. z o.o., CN=Firma Tradycyjna Polska Sp. z o.o. Root CA
````

Place all related files in the /ca folder. Use CA.crt for the name of CA certificate file. Issued certificates should contain (only and exactly) the following fields:

````
C=PL, O=Firma Tradycyjna Polska Sp. z o.o., CN=<FQDN>
````

Make sure all servers and the client applications used accept the certs issued by this CA.

2. **Make sure, the public services (DNS, mail, web) of the HQ site can accessible from the internet** ([NAT](IPTABLES/NAT/README.md)). Configure [firewall](IPTABLES/FIREWALL/README.md) with iptables. Incoming packets should be dropped by default. Allow minimal traffic for the services to work. Allow SSH traffic from everywhere. Make sure, that iptables persist across reboots.

3. **Ensure secure channel between the HQ and the datacentre sites** ([Site-to-Site VPN](VPN/Site-to-Site/README.md)). If this cannel broke, the clients of the HQ site can access the public services of the datacentre.

4. **Configure a [remote access VPN](VPN/Remote_Access/README.md) service for a remote workers**. Make sure, VPN clients can access to the same resources as the clients of the HQ site.



### hq-intra

1. **Deploy a directory service** with [LDAP protocol](LDAP/README.md). Create all objects listed in Appendix B.

   2. **Create a [failover DHCP cluster](DHCP/README.md) with hq-noc for the client network of HQ site**. HQ client subnet uses [DDNS](DHCP/+_UPDATE/README.md) so make sure that all A and PTR records are dynamically updated.

### hq-noc

1. Add 4 new 2GB HDD to a machine. **Configure software-based [RAID 5](RAID_5/README.md)** array and mount this to /share path.

2. **Configure [CIFS](test.md) service** for the profile directory of the corporate users. Use the /share/users/<username> as the path of the profile directories.

3. **Create a [failover DHCP cluster](test.md) with hq-intra**. See details there.

4. **Create monitoring service with [Cacti](test.md)**. Monitor the CPU, memory and disk usage of all servers on the HQ site with [SNMP](test.md). Send email alert to the admin@firmatpolska.pl if the memory usage of any server more then 80%.

5. **Configure [syslog](test.md) server** to collect logfiles from the servers of the HQ site.

   - Logs coming from hq-intra related to ``DHCP`` should be written to ``/log/dhcp.log``

   - Logs coming from dmz-host related to ``e-mail`` should be written to ``/log/mail.log``

   - ``All other incoming logs`` from the HQ site should be written to ``/log/dump.log``

### dmz-host

1. **Deploy a [DNS](test.md) server of the ``firmatpolska.pl`` domain**. Serves the reverse records of the HQ networks also.
   
    This server needs to reply to DNS requests from the other sites and from the Internet also, but not allow to serve a private IPs outside of HQ site. Create entries for all servers (both sites) and services.

2. **Configure [DDNS](test.md) for HQ client network.**

3. **Install and configure [web service](test.md)**. Serve the ``https://internal.firmatpolska.pl``. Use client certificate authentication. Only the users with a valid certificate signed by the company’s CA can access to this site.

4. **Configure [e-mail](test.md) service** to send and receive email for the firmatpolska.pl domain. Users access their mailboxes using TLS-secured IMAP (port 143) and send emails using STARTTLS secured SMTP (port 587). No unencrypted traffic from mailer clients are allowed. Both services require authentication. Port 25 is only used to accept mails from other SMTP servers (both encrypted and unencrypted)

### hq-clt01

1. Install a **[graphic environment](test.md)** of your choice.

2. **Configure [LDAP authentication](test.md)** using the LDAP server and make the CIFS-shared home folder of the logged in user available.

    Prevent user to use local user account to login to the system except root and LDAP users.

    The LDAP users which is logged in previously to this machine, can log in also when the LDAP server is not available.

3. **Install Thunderbird** e-mail client to use with admin@firmatpolska.pl. Send an e-mail message to maja.










#### Data Center

- fw-sddc
- iaac-mgmt
- bck-srv01..n
- frt-web01..n

#### Remote Worker

- ra-clt01