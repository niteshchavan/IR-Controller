# IR-Controller
Control raspberry pi with any remote 

# Source
https://peppe8o.com/setup-raspberry-pi-infrared-remote-from-terminal/

#Commands
sudo apt update

sudo nano /boot/config.txt

dtoverlay=gpio-ir,gpio_pin=17

sudo reboot

# Install ir-keytable
sudo apt install ir-keytable

# To read the current keymaps
sudo ir-keytable -r

# To clear all the keymaps
sudo ir-keytable -c 

# Check if remote is responding 
sudo ir-keytable -t 

# Change the prtotcol to nec if remote is not working
sudo ir-keytable -p nec

# make toml file 
sudo ir-keytable -w /pathToFile/your.toml

# my keymap attached
