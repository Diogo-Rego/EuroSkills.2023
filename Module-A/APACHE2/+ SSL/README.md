<p align="center">
  <a href="">
    <img src="../img/apache2+ssl.png" alt="APACHE2 + SSL" width="160" height="160">
  </a>
  <h1 align="center">APACHE2 + SSL</h1>
</p>

### Step 1: Obtain SSL/TLS Certificates

- Before adding certificates to Apache2, you need to obtain SSL/TLS certificates. You can obtain them from a trusted certificate authority (CA) or use a self-signed certificate for testing purposes. Here are the general steps for obtaining certificates:

    * Generate a private key: Use a tool like OpenSSL to generate a private key file (e.g., ``private.key``). Keep this key file secure.

    * Create a certificate signing request (CSR): Use the private key to generate a CSR file (e.g., ``certificate.csr``). The CSR contains information about your server and is used to request a certificate from a CA.

    * Submit the CSR to a CA: Submit the CSR to a trusted CA and follow their instructions to obtain the SSL/TLS certificate. The CA will typically provide you with a certificate file (e.g., ``certificate.crt``).

### Step 2: Enable SSL/TLS Module

- Apache2 needs the SSL/TLS module enabled to support HTTPS. Run the following command to enable the module:

```
sudo a2enmod ssl
```

### Step 3: Create a Certificate File

- Combine your SSL/TLS certificate (``certificate.crt``) and the CA's intermediate certificate(s) into a single file. You can use a text editor to concatenate the files. Save the combined file as ``yourdomain.crt``. For example:

```
cat certificate.crt intermediate.crt > yourdomain.crt
```

- If you have a bundle of intermediate certificates, make sure to include them in the concatenation.

### Step 4: Configure Apache2 to Use SSL/TLS

- Edit the virtual host configuration file for your domain (e.g., ``mydomain.conf``) that you created earlier. Add the following SSL/TLS-related directives inside the ``<VirtualHost>`` block:

```
<VirtualHost *:443>
    ServerName yourdomain.com
    ServerAlias www.yourdomain.com
    DocumentRoot /var/www/html

    SSLEngine on
    SSLCertificateFile /path/to/yourdomain.crt
    SSLCertificateKeyFile /path/to/private.key
    # Optional: SSLCertificateChainFile /path/to/intermediate.crt

    <Directory /var/www/html>
        Options FollowSymLinks
        AllowOverride All
        Require all granted
    </Directory>

    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
```

- Make sure to replace ``/path/to/`` with the actual paths to your certificate and private key files.

**Note:** If you have a separate intermediate certificate file, you can uncomment the ``SSLCertificateChainFile`` directive and provide the path to the intermediate certificate file.

### Step 5: Save the virtual host configuration file and exit the text editor.

### Step 6: Enable the SSL/TLS virtual host

- Run the following command to enable the SSL/TLS virtual host configuration:

```
sudo a2ensite mydomain.conf
```

### Step 7: Restart Apache2

- Restart Apache2 to apply the changes:

```
sudo service apache2 restart
```

### Step 8: Test HTTPS

- Open a web browser and enter your domain name with ``https://`` (e.g., ``https://yourdomain.com``). If the configuration is correct, you should see your website served over HTTPS.