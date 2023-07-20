## LDAP
````
apt-get -y install slapd ldap-utils
````
````
dpkg-reconfigure slapd
````
````
nano base.ldif
````
````
dn: ou=User,dc=example,dc=com
objectClass: organizationalUnit
ou: User
````
````
ldapadd -x -W -D 'cn=admin,dc=example,dc=com' -f base.ldif
````
````
vi paul.ldif
````
````
dn: uid=ldapuser,ou=People,dc=itzgeek,dc=local
objectClass: top
objectClass: account
objectClass: posixAccount
objectClass: shadowAccount
cn: ldapuser
uid: ldapuser
uidNumber: 9999
gidNumber: 100
homeDirectory: /home/ldapuser
loginShell: /bin/bash
userPassword: P@ssw0rd
````
````
ldapadd -x -W -D "cn=admin,dc=example,dc=com" -f paul.ldif
````
````
ldapsearch -x cn=paul -b dc=example,dc=com
````
````
apt-get -y install libnss-ldapd libpam-ldapdd ldap-utils nscd
````
````
dpkg-reconfigure libnss-ldapd
````
````
vi /etc/nsswitch.conf
````
````
passwd:         compat ldap
group:          compat ldap
shadow:         compat ldap
````
````
nano /etc/pam.d/common-session
````
````
session optional        pam_mkhomedir.so skel=/etc/skel umask=07
````