<p align="center">
  <a href="">
    <img src="../img/rsyslog.png" alt="RSYSLOG" width="160" height="160">
  </a>
  <h1 align="center">RSYSLOG</h1>
</p>

### Step 1: Set up the rsyslog server

- Install rsyslog: Ensure that rsyslog is installed on the server machine. Use the package manager specific to your Linux distribution to install it. For example, on Ubuntu, you can use the following command:

````
sudo apt install rsyslog
````

- Configure rsyslog to act as a server: Edit the rsyslog configuration file, typically located at ``/etc/rsyslog.conf``, using a text editor with root privileges.

Uncomment or add the following lines to enable network logging:

````
# Provides UDP syslog reception
module(load="imudp")
input(type="imudp" port="514")

# Provides TCP syslog reception
module(load="imtcp")
input(type="imtcp" port="514")
````

- Save the configuration file.

### Step 2: Restart rsyslog service

- Restart the rsyslog service to apply the changes. The command to restart the service varies depending on your Linux distribution. On Ubuntu, you can use

````
sudo service rsyslog restart
````

### Step 3: Configure the rsyslog client(s)

- Install rsyslog: Ensure that rsyslog is installed on the client machine(s) as well.

- Configure rsyslog to send logs to the server: Edit the rsyslog configuration file, typically located at ``/etc/rsyslog.conf``, using a text editor with root privileges.

  - Uncomment or add the following line to forward logs to the server:
 
````
*.* @server_ip_address:514
````

Replace ``server_ip_address`` with the IP address or hostname of the rsyslog server. The ``@`` symbol specifies the use of UDP for log forwarding. If you prefer TCP, use ``@@`` instead.

- Restart rsyslog service: Save the file and restart the rsyslog service on the client machine(s) to apply the configuration changes. Again, the command to restart the service depends on the Linux distribution. On Ubuntu, you can use:

````
sudo service rsyslog restart
````

### Step 4: Verify the configuration

- On the rsyslog server, monitor the log file you specified for received logs. In this example, you can use the following command to view incoming logs:

````
tail -f /var/log/syslog
````

- On the rsyslog client(s), generate log messages to test the setup. You can use the ``logger`` command to send test messages. For example:

````
logger "This is a test message"
````

- Check the log file on the server to verify that the log messages from the client(s) are being received and logged correctly.
