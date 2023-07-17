# SAMBA

Install Samba:

````
sudo apt install samba
````

Configure Samba:

- Open the Samba configuration file using a text editor. For example:

````
sudo nano /etc/samba/smb.conf
````

Find the [global] section in the configuration file. You can modify or add the following parameters according to your needs:

- Set the workgroup (optional):

````
workgroup = WORKGROUP
````

- Set the NetBIOS name (optional):

````
netbios name = YOUR_SERVER_NAME
````

- Set the server string (optional):

````
server string = Samba Server
````

- Set the security mode:

````
security = user
````

- Configure shared directories:

````
[share]
path = /path/to/shared/folder
writeable = yes
guest ok = yes
create mask = 0755
directory mask = 0755
````

Replace /path/to/shared/folder with the actual path to the folder you want to share. Adjust the permissions (create mask and directory mask) as needed.

Save the configuration file (Ctrl+O in nano) and exit the text editor (Ctrl+X).

Add Samba users:

- Create Samba users and set their passwords using the smbpasswd command. For example:

````
sudo smbpasswd -a username
````

Replace username with the desired username.

Restart the Samba service:

````
sudo service smbd restart
````

Once the Samba server is configured and running, other devices on the network should be able to access the shared folder using the server's IP address or hostname. In a file explorer or file manager, you can enter \\your_server_ip or \\your_server_hostname in the address bar to access the shared folder.

Note: Make sure your firewall settings allow Samba traffic if you have a firewall enabled on your Linux system.


ldap suffix = dc=example,dc=com
ldap user suffix = ou=Users
ldap group suffix = ou=Groups
ldap machine suffix = ou=Computers
ldap admin dn = cn=admin,dc=example,dc=com