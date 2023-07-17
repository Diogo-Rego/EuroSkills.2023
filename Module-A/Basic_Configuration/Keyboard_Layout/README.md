<p align="center">
  <a>
    <img src="../../img/keyboard_layouts.png" alt="Keyboard Layout" width="160" height="160">
  </a>
  <h1 align="center">Keyboard Layout</h1>
</p>

### Step 1: Check the available keyboard layouts by running

````
sudo dpkg-reconfigure keyboard-configuration
````

1. You'll be presented with a configuration dialog that allows you to select your keyboard layout, keyboard model, and other options. Use the arrow keys to navigate and the spacebar to select options.

2. Once you have selected the desired keyboard layout and options, save the changes and exit the configuration dialog.

3. After making the changes, apply the new configuration by running:

````
sudo service keyboard-setup restart
````

OR

````
sudo reboot
````