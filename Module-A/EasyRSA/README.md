<p align="center">
  <a href="https://github.com/Diogo-Rego/EuroSkills.2023/tree/main/Module-A/EasyRSA#easyrsa">
    <img src="../img/EasyRSA.png" alt="EasyRSA" width="160" height="160">
  </a>
  <h1 align="center">EasyRSA</h1>
</p>

### Step 1: Install EasyRSA on your Debian system if you haven't already. You can typically do this by installing the ``easy-rsa`` package:

```
sudo apt-get install easy-rsa
```

### Step 2: Once installed, copy the EasyRSA directory for other directory:

```
cp -R /usr/share/easy-rsa/ /etc/
```

### Step 3: Navigate to the EasyRSA directory:

```
cd /etc/easy-rsa/
```

### Step 4: Copy the ``vars.example`` file to a new file (let's call it ``vars``):

```
cp vars.example vars
```

### Step 5: Open the ``vars`` file using a text editor:

```
nano vars
```

### Step 6: Modify the variables in the ``vars`` file according to your requirements. For example, you may need to set the following variables:

```
set_var EASYRSA_DN      "org"

set_var EASYRSA_REQ_COUNTRY     "PL"
set_var EASYRSA_REQ_PROVINCE    ""
set_var EASYRSA_REQ_CITY        ""
set_var EASYRSA_REQ_ORG "Firma Tradycyjna Polska Sp. z o.o."
set_var EASYRSA_REQ_EMAIL       ""
set_var EASYRSA_REQ_OU          ""

set_var EASYRSA_REQ_CN          "Firma Tradycyjna Polska Sp. z o.o. Root CA"

set_var EASYRSA_BATCH           "yes"
```

- Adjust the values to match your desired organization details.

### Step 7: Save and exit the ``vars`` file.

### Step 8: Initialize the EasyRSA environment and build the Certificate Authority (CA):

```
./easyrsa init-pki
./easyrsa build-ca
```

- This command will generate a server certificate signing request (CSR) without a passphrase.

### Step 9: Sign the certificate using the CA:

* For Server:

```
./easyrsa build-server-full srv.name nopass
```

* For Client:

```
./easyrsa build-clint-full cli.name nopass
```

### Step 10: Sign a certificate signing request (CSR) with the Common Name (CN) "www.test.pt" and an additional Subject Alternative Name (SAN):

```
./easyrsa --subject-alt-name="DNS:www.test.pt" sign-req server www.test.pt
```