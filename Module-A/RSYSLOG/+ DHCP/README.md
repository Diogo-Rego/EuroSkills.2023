<p align="center">
  <a href="">
    <img src="../img/rsyslog+dhcp.png" alt="RSYSLOG + DHCP" width="160" height="160">
  </a>
  <h1 align="center">RSYSLOG + DHCP</h1>
</p>

### Step 1: Open the rsyslog configuration file

- Locate the rsyslog configuration file, typically located at ``/etc/rsyslog.conf`` or ``/etc/rsyslog.d/50-default.conf``. Use a text editor with root privileges to open the file.

- Now that the DHCP server is configured to send logs to the ``local7`` facility, you need to configure rsyslog to capture and separate these logs.

````
local7.* /var/log/dhcp.log
````

- Define separate log destinations for DHCP: Add the following line at the end of the configuration file to specify the log destination for DHCP logs:

````
if $programname == 'dhcpd' then /var/log/dhcp.log
````

This line tells rsyslog to redirect logs from the ``dhcpd`` program to ``/var/log/dhcp.log``.

- Save the configuration file.

### Step 2: Restart rsyslog service

- Restart the rsyslog service to apply the changes. The command to restart the service varies depending on your Linux distribution. On Ubuntu, you can use:

````
sudo service rsyslog restart
````

### Step 3: Verify DHCP logging

- Ensure that your DHCP server is configured to log to the syslog facility. The exact steps may vary depending on your DHCP server software. In most cases, you can find the logging configuration in the DHCP server's configuration file (e.g., ``/etc/dhcp/dhcpd.conf``). Look for a directive similar to:

````
log-facility local7;
````

Make sure the log facility matches the facility used in the rsyslog configuration (``local7`` in this example).

### Step 4: Restart the DHCP server

- Restart the DHCP server service to apply the changes. The method for restarting the DHCP server varies depending on the distribution and DHCP server software. For example, on Ubuntu, you can use the following command:

````
sudo service isc-dhcp-server restart
````
