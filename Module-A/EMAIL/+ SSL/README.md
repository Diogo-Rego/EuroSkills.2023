# EMAIL + SSL

### Step 1: Generate or Obtain an SSL/TLS Certificate

- You can generate a self-signed certificate for testing purposes using OpenSSL:

```
sudo openssl req -x509 -nodes -newkey rsa:2048 -keyout /etc/ssl/private/mail.key -out /etc/ssl/certs/mail.crt -days 365
```

- If you have a certificate from a trusted certificate authority (CA), obtain the certificate and the corresponding private key.

### Step 2: Configure Postfix

- Edit the Postfix main configuration file:

```
sudo nano /etc/postfix/main.cf
```

- Add or modify the following lines to enable TLS:

```
smtpd_tls_cert_file = /etc/ssl/certs/mail.crt
smtpd_tls_key_file = /etc/ssl/private/mail.key
smtpd_use_tls = yes
smtpd_tls_auth_only = yes
smtpd_tls_security_level = may
smtpd_tls_loglevel = 1
smtp_tls_security_level = may
smtp_tls_loglevel = 1
```

- Save the file and exit the text editor.

### Step 3: Configure Dovecot

- Edit the Dovecot configuration file:

```
sudo nano /etc/dovecot/conf.d/10-ssl.conf
```

- Uncomment or modify the following lines:

```
ssl = yes
ssl_cert = </etc/ssl/certs/mail.crt
ssl_key = </etc/ssl/private/mail.key
```

- Save the file and exit the text editor.

### Step 4: Restart Services

- Restart Postfix and Dovecot to apply the changes:

```
sudo systemctl restart postfix
sudo systemctl restart dovecot
```

- TLS encryption is now enabled for your Postfix email server. It's important to note that using a self-signed certificate may generate warnings in email clients since it is not issued by a trusted CA. For production environments, consider obtaining a certificate from a trusted CA to avoid these warnings.