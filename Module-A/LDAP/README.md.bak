<p align="center">
  <a>
    <img src="../../img/banner.png" alt="LDAP" width="160" height="160">
  </a>
  <h1 align="center">LDAP</h1>
</p>

### Step 1: 
 - Install LDAP 
````
apt install ldap-utils slapd


apt install libnss-ldap libpam-ldap
````

 - You get prompted to set up your administrator password. Enter a new password and then confirm the password.

 - Then reconfigure the default entries:

```
dpkg-reconfigure slapd
```
 - Edit the LDAP configuration file 

````
sudo nano /etc/ldap/ldap.conf
````

 - Uncomment and change the following contents:
````
BASE     dc=example,dc=com
URI      ldap://ldap.example.com ldap://ldap-master.example.com:666
````

 - Create a password for your root use
````
slappasswd
````
{SSHA}04LMaQWmKy5WXDySz/cVk28q5iP5DEAY
 - Create a rootpw.ldif file
````
nano rootpw.ldif
````
Enter the following contents:

````
dn: olcDatabase={0}config,cn=config
changetype: modify
add: olcRootPW
olcRootPW: {SSHA}yh/GrT7AsObYUoHu89ynjzOljpBP10sp
````

Replace the {SSHA}yh/GrT7AsObYUoHu89ynjzOljpBP10sp with the hash that you obtained in the slappasswd command.


ldapadd -Y EXTERNAL -H ldapi:/// -f rootpw.ldif


ldapadd -Y EXTERNAL -H ldapi:/// -f /etc/ldap/schema/cosine.ldif
ldapadd -Y EXTERNAL -H ldapi:/// -f /etc/ldap/schema/nis.ldif
ldapadd -Y EXTERNAL -H ldapi:/// -f /etc/ldap/schema/inetorgperson.ldif
ldapadd -Y EXTERNAL -H ldapi:/// -f /etc/ldap/schema/openldap.ldif
ldapadd -Y EXTERNAL -H ldapi:/// -f /etc/ldap/schema/dyngroup.ldif





nano manager.ldif




dn: olcDatabase={1}monitor,cn=config
changetype: modify
replace: olcAccess
olcAccess: {0}to * by dn.base="gidNumber=0+uidNumber=0,cn=peercred,cn=external,cn=auth" read by dn.base="cn=Manager,dc=rpa,dc=ibm,dc=com" read by * none

dn: olcDatabase={2}mdb,cn=config
changetype: modify
replace: olcSuffix
olcSuffix: dc=rpa,dc=ibm,dc=com

dn: olcDatabase={2}mdb,cn=config
changetype: modify
replace: olcRootDN
olcRootDN: cn=Manager,dc=rpa,dc=ibm,dc=com

dn: olcDatabase={2}mdb,cn=config
changetype: modify
add: olcRootPW
olcRootPW: {SSHA}yh/GrT7AsObYUoHu89ynjzOljpBP10sp

dn: olcDatabase={2}mdb,cn=config
changetype: modify
add: olcAccess
olcAccess: {0}to attrs=userPassword,shadowLastChange by dn="cn=Manager,dc=rpa,dc=ibm,dc=com" write by anonymous auth by self write by * none
olcAccess: {1}to dn.base="" by * read
olcAccess: {2}to * by dn="cn=Manager,dc=rpa,dc=ibm,dc=com" write by * read



Replace the olcRootPW with the password hash that you obtained with the slappasswd tool.
Replace the dc=rpa,dc=ibm,dc=com with your own base DN.


Tip:On Ubuntu, you might need to change the olcDatabase={2}mdb to olcDatabase={1}mdb. Check the name of the file with the output of the following command:
ls /etc/ldap/slapd.d/cn\=config/


ldapmodify -Y EXTERNAL -H ldapi:/// -f manager.ldif




Create a new LDIF file to create your organization groups:

nano org.ldif


dn: dc=rpa,dc=ibm,dc=com
objectClass: top
objectClass: dcObject
objectclass: organization
o: IBM RPA Server
dc: rpa

dn: cn=Manager,dc=rpa,dc=ibm,dc=com
objectClass: organizationalRole
cn: Manager
description: LDAP Manager

dn: ou=rpausers,dc=rpa,dc=ibm,dc=com
objectClass: organizationalUnit
ou: rpaUsers


Apply the contents with your Manager user:
ldapadd -x -D cn=Manager,dc=rpa,dc=ibm,dc=com -W -f org.ldif


nano addUserName.ldif

dn: cn=User Name,dc=rpa,dc=ibm,dc=com
changetype: add
objectClass: inetOrgPerson
objectClass: organizationalPerson
objectClass: person
objectClass: top
uid: username
cn: User Name
sn: Name
displayName: User Name
mail: username@example.com
userPassword: {SSHA}xxxxxxxxxxxxxxxxxxxxxxxxxxxxxx


Replace dc=rpa,dc=ibm,dc=com with your base DN.
In sn enter the user's surname.
In uid, enter the user's username.
In displayName, enter the user's display name.
In mail, enter the user's email address.
In userPassword, enter the hash of the user's password obtained with the slappasswd command.

systemctl start slapd.service

systemctl enable slapd.service