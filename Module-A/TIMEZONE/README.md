<p align="center">
  <a href="www.google.com">
    <img src="../img/time-zone.jpg" alt="TIMEZONE" width="160" height="160">
  </a>
  <h1 align="center">Configuration the TimeZone</h1>
</p>


1. To view the list of available timezones, run the following command:

```
timedatectl list-timezones
```
This command will display a long list of timezones. Scroll through the output to find the desired timezone.

2. Once you have identified the desired timezone, use the following command to set it:

```
sudo timedatectl set-timezone [timezone]
```
Replace ``[timezone]`` with the timezone you want to configure. For example, to set the timezone to "Europe/Warsaw," the command would be:

3. After running the command, timedatectl will update the system's timezone configuration.

4. To verify the changes, run the following command:

```
timedatectl
```
