<p align="center">
  <a href="https://github.com/Diogo-Rego/EuroSkills.2023/tree/main/Module-A/BANNER%20-%20OK#banner">
    <img src="../img/banner.png" alt="BANNER" width="160" height="160">
  </a>
  <h1 align="center">BANNER</h1>
</p>

### Step 1: Create the banner files

- Using a text editor, create the banner files with the desired content. You will need separate files for the login banner and the remote login (SSH) banner.

- For the login banner:

```
sudo nano /etc/issue
```

- For the SSH banner:

```
sudo nano /etc/issue.net
```

- Add the desired content to each file. For example, you can include a message or a warning. Here's an example of a login banner:

```
Welcome to My Debian Server!
Unauthorized access is strictly prohibited.
```

- And here's an example of an SSH banner:

```
** Authorized access only **
All activities may be monitored and recorded.
```

- Save the files and exit the text editor.

### Step 2: Configure PAM to display the banner

- PAM (Pluggable Authentication Modules) controls the login process on Debian. Edit the PAM configuration file:

```
sudo nano /etc/pam.d/login
```

- Add the following line at the top of the file:

```
auth       required     pam_issue.so issue=/etc/issue
```

- Save the file and exit the text editor.

### Step 3: Configure SSH to display the banner

- For SSH, you need to modify the SSH daemon configuration file. Edit the SSH configuration file:

```
sudo nano /etc/ssh/sshd_config
```

- Find the line that starts with ``#Banner`` and remove the ``#`` at the beginning of the line. Then, specify the path to the SSH banner file (``/etc/issue.net``) after the ``Banner`` keyword. It should look like this:

```
Banner /etc/issue.net
```

- Save the file and exit the text editor.

### Step 4: Restart services

- Restart the login service and SSH daemon to apply the changes:

```
sudo systemctl restart systemd-logind
sudo systemctl restart ssh
```

- The login and SSH banners will now be displayed when users try to log in.

**Note:** It's important to ensure that the content of the banners complies with your organization's policies and legal requirements. Additionally, keep in mind that these banners are displayed in plaintext and can be read by anyone accessing the login or SSH prompt. Avoid including sensitive information or personally identifiable information (PII) in the banners.