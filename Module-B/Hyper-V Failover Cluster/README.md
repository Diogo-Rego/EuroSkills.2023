# Hyper-V Failover Cluster



Enable-PSRemoting -Force


Get-Service -Name WinRM

Start-Service -Name WinRM

Next, run the following command to set the WinRM service to start automatically:
Set-Service -Name WinRM -StartupType Automatic

To configure the WinRM service to allow remote connections, run the command:
Set-Item WSMan:\localhost\Service\AllowRemoteConnection -Value $true
