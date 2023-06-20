<p align="center">
  <a href="https://github.com/Diogo-Rego/EuroSkills.2023/tree/main/Module-A/TIMEZONE%20-%20OK#configuration-the-timezone">
    <img src="../img/time-zone.png" alt="TIMEZONE" width="160" height="160">
  </a>
  <h1 align="center">Configuration the TimeZone</h1>
</p>


### Step 1: To view the list of available timezones, run the following command:

```
timedatectl list-timezones
```
- This command will display a long list of timezones. Scroll through the output to find the desired timezone.

### Step 2: Once you have identified the desired timezone, use the following command to set it:

```
sudo timedatectl set-timezone [timezone]
```

- Replace ``[timezone]`` with the timezone you want to configure. For example, to set the timezone to "Europe/Warsaw," the command would be:

### Step 3: After running the command, timedatectl will update the system's timezone configuration.

### Step 4: To verify the changes, run the following command:

```
timedatectl
```
