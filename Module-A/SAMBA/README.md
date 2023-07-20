## SAMBA + LDAP

### -SRV 
````
apt-get install samba smbldap-tools
````

````
mkdir /etc/ldap/schema/
````
````
cp /usr/share/doc/samba/examples/LDAP/samba.schema /etc/ldap/schema
````

````
nano /etc/samba/smb.conf
````
````
[global]
   passdb backend = ldapsam:ldap://X.X.X.X
   ldap suffix = dc=example,dc=com
   ldap user suffix = ou=example
   ldap group suffix = ou=example
   ldap admin dn = cn=admin,dc=example,dc=com
   include /etc/ldap/schema/samba.schema
````
````
smbpasswd –w user1 
smbpasswd -a user1 
````
````
nano /etc/samba/smb.conf
````
````
[share]
   path = /local_folder
   browseable = yes/no
   security = @group/user
   writeable = yes/no
   read only = yes/no
   inherit permissions = yes/no
   inherit owner = yes/no
````
````
Chmod -R 1777 /local_folder
chown *user /local_folder
````
````
systemctl restart smbd
systemctl enable smbd
````

### -CLI
````
apt-get install smbclient cifs-utils
````
````
smbclient //X.X.X.X/[share_name] -U *(user)
````
````
nano /etc/fstab
````
````
//X.X.X.X/SHARE_NAME	/LOCAL_FOLDER	CIFS	username=*,password=* 0 0 defaults 
````