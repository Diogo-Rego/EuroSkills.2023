<p align="center">
  <a href="./README.md">
    <img src="img/Linux_Environment.png" alt="Linux Environment" width="160" height="160">
  </a>
  <h1 align="center">Module A – Linux Environment</h1>
</p>

# INTRODUCTION

The competition has a fixed start and finish time. You must decide how to best divide your time.

**Please carefully read the following instructions!**

When the competition time ends, please leave your station in a running state. The assessment will be
done in the state as it is. **No reboot will be initiated as well as powered off machines will not
be powered on!**

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

> You will find the topology and the listing of used IP addresses at the end of this document. The list of
the users to be created can be found there too.

# PREINSTALLED RESOURCES

> Every system in this task uses **Debian 11**. Every VM you see in the topology chart at the end of this
document is preinstalled on the physical host, named accordingly. The hosts use VMware ESXi as a
virtualisation platform and you can connect to the resources using your laptops with vSphere Web
Client or VMware Workstation also.

**You can connect to the ESXi host with esxi.local URL.**

> The preinstalled VMs contain only the base system and few additional packages (see in the software
section), you can install additional software using virtual optical disks.

# SOFTWARE

> For testing purpose, all VM has been installed with the following test tools: 

```
smbclient, curl, lynx, dnsutils, ldap-utils, ftp, lftp, wget, ssh, nfs-common, rsync, telnet, traceroute, tcptraceroute,
tcpdump, net-tools, cifs-utils.
```

**You can find a Debian install ISOs in the datastore.**

# INDRUSTY COMPLIANCE

> The test project does not always give you an exact specification. In these situations you have the
chance to choose which software to use, which path to follow - you will find information at the tasks
about the paths you can choose from. The more sophisticated a solution is the better mark you are
going to get for it.

# DESCRIPTION OF PROJECT AND TASKS

> You are a new IT Engineer of the Firma Tradycyjna Polska Sp. z o.o. company. The goal of your next
project is to build the whole IT infrastructure of the company.

# General Configuration

Set up all the resources with the following:

- [hostname,](test.md)


#### Corporate HQ

- fw-hq
  - [Easy-RSA](www.google.com)
  - [Firewall](www.google.com)
  - [NAT](www.google.com)
  - [VPN (Site-to-Site)](www.google.com)
  - [VPN (Remote Access)](www.google.com)
- hq-intra
  - [a](a)
  - [a](a)
  - [a](a)
  - [a](a)
  - [a](a)
- hq-noc
  - [a](a)
  - [a](a)
  - [a](a)
  - [a](a)
  - [a](a)
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