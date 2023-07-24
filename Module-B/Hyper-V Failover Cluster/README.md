to allow dk-srv1 to add the core to the failover cluster
````
Start-Service RemoteRegistry
Set-Service -Name RemoteRegistry -StartupType Automatic
````

sconfig
7
e
2


















not working for some reason 
````
Get-Service RemoteAccess
Start-Service RemoteAccess
````







Start-Service RpcSs

Start-Service RpcEptMapper

Set-Service -Name WinRM -StartupType Automatic


Set-Item WSMan:\localhost\Service\AllowRemoteConnection -Value $true

Enable-PSRemoting -Force

Get-Service -Name WinRM

Start-Service -Name WinRM

netsh advfirewall firewall set rule group="remote desktop" new enable=Yes

Create the Firewall Rule: Use the netsh advfirewall command to add a new inbound rule for port 135:

netsh advfirewall firewall add rule name="DCOM-In" dir=in action=allow protocol=TCP localport=135

Optional: Enable RPC Dynamic Ports: In some cases, applications or services might use dynamic RPC ports. If you need to enable dynamic RPC port allocation, use the following commands:

netsh int ipv4 set dynamicport tcp start=49152 num=16384
netsh int ipv4 set dynamicport udp start=49152 num=16384

Restart the Firewall Service: After making changes to the firewall rules, it's a good practice to restart the Windows Firewall service to apply the changes:

Restart-Service -Name "MpsSvc"







open mmc 

services to check if the services are enabled correctly 

then go mmc again and open the group polyci object fo to 

Computer Configuration>Administrative Templates>Network>Network Connections>Windows Firewall

Double-click Domain Profile>Windows Firewall: Allow inbound remote administration exception

and 

Double-click Domain Profile>Windows Firewall: Allow inbound remote desktop exception

Select Enabled

Click Apply

Click OK