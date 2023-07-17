
### Corporate HQ

- fw-hq

  - <sub><input type="checkbox"/></sub> hostname
  - network configuration
  - time zone
  - keyboard layout
  - install SSH server and allow root password access
  - root certificate authority (Easy-RSA)
  - firewall (iptables)
  - nat (iptables and netfiter-persistent)
  - site-to-site vpn
  - remote access vpn

- hq-intra

  - hostname
  - network configuration
  - time zone
  - keyboard layout
  - install SSH server and allow root password access
  - dhcp
    - dhcp failover
    - dhcp ddns
  - ldap

- hq-noc

  - hostname
  - network configuration
  - time zone
  - keyboard layout
  - install SSH server and allow root password access
  - raid 5
  - samba
  - dhcp
    - dhcp failover
    - dhcp ddns
  - cacti
    - snmp
  - syslog

- dmz-host

  - hostname
  - network configuration
  - time zone
  - keyboard layout
  - install SSH server and allow root password access
  - dns
    - ddns
  - apache2
  - postfix and dovecot

- hq-clt01

  - hostname
  - network configuration
  - time zone
  - keyboard layout
  - install SSH server and allow root password access
  - graphic environment
  - ldap authentication
  - thunderbird

### Data Center

- fw-sddc

  - hostname
  - network configuration
  - time zone
  - keyboard layout
  - install SSH server and allow root password access
  - site-to-site vpn
  - firewall (nstables)
  - nat (nstables)

- iaac-mgmt

  - [ ] hostname
  - network configuration
  - time zone
  - keyboard layout
  - install SSH server and allow root password access
  - ansible
    - playbooks

      - frt-web01..n

        - hostname
        - time zone
        - keyboard layout
        - install SSH server and allow root password access
        - firewall
        - apache2
        - keepalived
          - vrrp
          - haproxy

      - bck-srv01..n
      
        - hostname
        - time zone
        - keyboard layout
        - install SSH server and allow root password access
        - firewall
        - apache2
        - ftp
        - sftp

### Remote Worker

- ra-clt01

  - graphic environment
  - ldap authentication
  - remote access vpn
