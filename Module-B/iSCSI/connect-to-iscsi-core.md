automatically start the iscsi iniciator when the pc start  
```
Set-Service -Name msiscsi -StartupType Automatic
```
start the iscsi iniciator service 
```
Start-Service msiscsi
```
discover the iscsi target 
```
New-iscsitargetportal -targetportaladdress <IP address>
```
connect to the iscsi target 
```
Connect-IscsiTarget -nodeaddress iqn.2005-10.org.freenas.ctl:quorum -IsPersistent $true -IsMultipathEnabled $true -InitiatorPortalAddress 10.0.0.70 -TargetPortalAddress 10.0.0.1
```
veriy if the iscsi target is online 
```
Get-iSCSItarget
```

verify if the disk is online 
```
diskpart 
list disk 
```
if the disk is offline 
```
select disk <iscsi disk>
online disk 
```

see if the disk is formated 
```
list volume 
```

if you can't see the iscsi volume then format the disk 
```
attributes disk clear readonly
clean
create partition primary
format fs=ntfs quick
assign letter=S
```
if you want to change the letter of the disk and it is formated you need to select the volume to change the letter no the disk 
