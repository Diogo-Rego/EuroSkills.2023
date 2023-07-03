<p align="center">
  <a href="">
    <img src="../img/rsyslog+mail.png" alt="RSYSLOG + MAIL" width="160" height="160">
  </a>
  <h1 align="center">RSYSLOG + MAIL</h1>
</p>

### Step 1: Open the rsyslog configuration file

- Locate the rsyslog configuration file, typically located at ``/etc/rsyslog.conf`` or ``/etc/rsyslog.d/50-default.conf``. Use a text editor with root privileges to open the file.

- Define separate log destinations for Postfix: Add the following line at the end of the configuration file to specify the log destination for Postfix logs:

````
if $programname == 'postfix' then /var/log/postfix.log
& stop
````

This line tells rsyslog to redirect logs from the ``postfix`` program to ``/var/log/postfix.log``.

- Save the configuration file.

### Step 2: Restart rsyslog service

- Restart the rsyslog service to apply the changes. The command to restart the service varies depending on your Linux distribution. On Ubuntu, you can use:

````
sudo service rsyslog restart
````

Verify Postfix logging: Ensure that your Postfix configuration is set to log to the syslog facility. The logging configuration can typically be found in the Postfix configuration file (e.g., ``/etc/postfix/main.cf``). Look for a line similar to:

````
syslog_name = postfix
````

Make sure the ``syslog_name`` matches the program name used in the rsyslog configuration (``postfix`` in this example).

### Step 3: Restart Postfix

- Restart the Postfix service to apply the changes made in its configuration file. The method for restarting Postfix varies depending on the distribution.

````
sudo service rsyslog restart
````
