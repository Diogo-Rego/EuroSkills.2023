<p align="center">
  <a>
    <img src="../../img/hostname.png" alt="HOSTNAME" width="160" height="160">
  </a>
  <h1 align="center">HOSTNAME</h1>
</p>

### Step 1: To set a new hostname, use the ``hostnamectl`` command with superuser privileges

````
sudo hostnamectl set-hostname new-hostname
````

Replace **'new-hostname'** with the desired hostname.

1. After running the command, you might need to restart your system for the changes to take effect:

````
sudo reboot
````

After the reboot, your Debian machine should be using the new hostname. To verify the new ``hostname``, you can use the hostname command:

````
hostname
````
