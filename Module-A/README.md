<p align="center">
  <a href="./README.md">
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

- [hostname,](test.md)
- [network configuration,](test.md)
- [time zone,](test.md)
- [keyboard layout,](test.md)
- [install SSH server and allow root password access](test.md) (for the easiest testing).

# Corporate HQ

This is the company’s headquarters site with limited server services and clients.

### fw-hq

> This is the edge router and firewall of the HQ site. For this reason, it should allow devices to reach each other between network segments and the Internet.

You must configure the services of this server according to the following requirements.

1. **Create a root certificate authority** ([Easy-RSA](test.md)). Use the next parameters:

````
C=PL, O=Firma Tradycyjna Polska Sp. z o.o., CN=Firma Tradycyjna Polska Sp. z o.o. Root CA
````

Place all related files in the /ca folder. Use CA.crt for the name of CA certificate file. Issued certificates should contain (only and exactly) the following fields:

````
C=PL, O=Firma Tradycyjna Polska Sp. z o.o., CN=<FQDN>
````

Make sure all servers and the client applications used accept the certs issued by this CA.

2. **Make sure, the public services (DNS, mail, web) of the HQ site can accessible from the internet** ([NAT](test.md)). Configure [firewall](test.md) with iptables. Incoming packets should be dropped by default. Allow minimal traffic for the services to work. Allow SSH traffic from everywhere. Make sure, that iptables persist across reboots.

3. **Ensure secure channel between the HQ and the datacentre sites** ([Site-to-Site VPN](test.md)). If this cannel broke, the clients of the HQ site can access the public services of the datacentre.

4. **Configure a [remote access VPN](test.md) service for a remote workers**. Make sure, VPN clients can access to the same resources as the clients of the HQ site.



### hq-intra

1. **Deploy a directory service** with [LDAP protocol](test.md). Create all objects listed in Appendix B.

2. **Create a [failover DHCP cluster](test.md) with hq-noc for the client network of HQ site**. HQ client subnet uses [DDNS](test.md) so make sure that all A and PTR records are dynamically updated.

### hq-noc

1. Add 4 new 2GB HDD to a machine. **Configure software-based [RAID 5](test.md)** array and mount this to /share path.

2. **Configure [CIFS](test.md) service** for the profile directory of the corporate users. Use the /share/users/<username> as the path of the profile directories.

3. **Create a [failover DHCP cluster](test.md) with hq-intra**. See details there.

4. **Create monitoring service with [Cacti](test.md)**. Monitor the CPU, memory and disk usage of all servers on the HQ site with [SNMP](test.md). Send email alert to the admin@firmatpolska.pl if the memory usage of any server more then 80%.

5. **Configure [syslog](test.md) server** to collect logfiles from the servers of the HQ site.

   - Logs coming from hq-intra related to ``DHCP`` should be written to ``/log/dhcp.log``
   - 
   - Logs coming from dmz-host related to ``e-mail`` should be written to ``/log/mail.log``
   - 
   - ``All other incoming logs`` from the HQ site should be written to ``/log/dump.log``





- dmz-host
  - [a](a)
  - [a](a)
  - [a](a)
  - [a](a)
  - [a](a)
- hq-clt01
  - [a](a)
  - [a](a)
  - [a](a)
  - [a](a)
  - [a](a)

#### Data Center

- fw-sddc
- laac-mgmt
- bck-srv01..n
- frt-web01..n

#### Remote Worker

- ra-clt01