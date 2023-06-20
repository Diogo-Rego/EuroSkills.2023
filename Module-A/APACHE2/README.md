<p align="center">
  <a href="">
    <img src="../img/apache2.png" alt="APACHE2" width="160" height="160">
  </a>
  <h1 align="center">APACHE2</h1>
</p>

### Step 1: Install Apache2

```
sudo apt install apache2
```

### Step 2: Locate the Apache2 Document Root

- Apache2 serves files from a directory known as the Document Root. By default, the Document Root is ``/var/www/html`` on Ubuntu and Debian. You can place your web page files in this directory or modify the Document Root as per your requirements.

### Step 3: Create your web page

- Use a text editor to create your web page file. For example, you can use nano to create a new HTML file named ``index.html``:

```
sudo nano /var/www/html/index.html
```

- Inside the file, add your HTML content. Here's a simple example:

```
<!DOCTYPE html>
<html>
<head>
    <title>My Web Page</title>
</head>
<body>
    <h1>Welcome to My Web Page</h1>
    <p>This is a sample web page.</p>
</body>
</html>
```

### Step 4: Save the file and exit the text editor.

### Step 5: Set appropriate file permissions

- Ensure that the file has appropriate read permissions so that Apache2 can serve it. In most cases, the default permissions are sufficient. You can use the following command to ensure the file has the correct permissions:

```
sudo chmod 644 /var/www/html/index.html
```

### Step 6: Start/restart Apache2

- If Apache2 is not already running, start it using the appropriate command for your operating system. For example, on Ubuntu or Debian, you can use:

```
sudo service apache2 start
```

- If Apache2 is already running, you can restart it with:

```
sudo service apache2 restart
```

### Step 7: Access your web page

- Open a web browser and enter your server's IP address or domain name in the address bar. You should see your web page displayed.