# IR-Controller
Control raspberry pi with any remote 

# Source
https://peppe8o.com/setup-raspberry-pi-infrared-remote-from-terminal/

https://blog.gordonturner.com/2020/05/31/raspberry-pi-ir-receiver/

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

# Move your toml to make it permenant
cp /nitesh/ir-remote/key.toml /etc/rc_keymaps/

 nano /etc/rc_maps.cfg

# add below line

 *       *                        key.toml

sudo ir-keytable -a /etc/rc_maps.cfg -s rc0

nano /etc/rc.local

# add before exit 0

ir-keytable -a /etc/rc_maps.cfg -s rc0

exit 0

# my keymap attached copy both 
chmod u+x /nitesh/ir-remote/ir-remote

# Next is maping keys to custom scripts/ commands
# create a script fro example 

nano /nitesh/ir-remote/kill-youtube

``` 
#!/bin/bash

sudo killall chromium-browser
```

> Change ownership and make executable:

```
sudo chown pi.pi /nitesh/ir-remote/kill-youtube
sudo chmod u+x /nitesh/ir-remote/kill-youtube
sudo chmod +x /nitesh/ir-remote/kill-youtube
```

The triggerhappy service is used, it can map events to scripts and is installed by default on Raspbian.

nano /lib/systemd/system/triggerhappy.service

and change from --user nobody to --user root this will give permission to run all as root

ExecStart=/usr/sbin/thd --triggers /etc/triggerhappy/triggers.d/ --socket /run/thd.socket --user root --deviceglob /dev/input/event*

systemctl daemon-reload && systemctl restart triggerhappy.service

# Edit

> nano /etc/triggerhappy/triggers.d/custom-key.conf

# Paste below save and exit

KEY_EXIT                   1       /nitesh/ir-remote/kill-youtube

sudo systemctl restart triggerhappy


