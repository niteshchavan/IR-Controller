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

# my keymap attached copy both 
chmod u+x /nitesh/ir-remote/ir-remote

# Next is maping keys to custom scripts/ commands
The triggerhappy service is used, it can map events to scripts and is installed by default on Raspbian.

nano /lib/systemd/system/triggerhappy.service

and change from --user nobody to --user root this will give permission to run all as root

ExecStart=/usr/sbin/thd --triggers /etc/triggerhappy/triggers.d/ --socket /run/thd.socket --user root --deviceglob /dev/input/event*

systemctl daemon-reload && systemctl restart triggerhappy.service

#edit

nano /etc/triggerhappy/triggers.d/custom-key.conf

#Paste below save and exit

KEY_EXIT                   1       /nitesh/ir-remote/kill-youtube

sudo systemctl restart triggerhappy


