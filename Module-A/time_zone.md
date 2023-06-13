# Configuration the timezone

1. To view the list of available timezones, run the following command:

```
timedatectl list-timezones
```
This command will display a long list of timezones. Scroll through the output to find the desired timezone.

2. Once you have identified the desired timezone, use the following command to set it:

```
sudo timedatectl set-timezone [timezone]
```
Replace ``[timezone]`` with the timezone you want to configure. For example, to set the timezone to "America/New_York," the command would be:

3. After running the command, timedatectl will update the system's timezone configuration.

4. To verify the changes, run the following command:

```
timedatectl
```

The output will display the current system time, date, and timezone, confirming that the timezone has been successfully configured.