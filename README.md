# hid-n-seek
Keyboard and Mouse Proxy for computer shortcuts with a Raspberry PI Zero 

## Setup PI Zero
Reference https://gist.github.com/gbaman/975e2db164b3ca2b51ae11e45e8fd40a

1. Flash Raspbian Stretch on SD card.

2. Once Raspbian is flashed, open up the boot partition (in Windows Explorer, Finder etc) and add to the bottom of the config.txt file dtoverlay=dwc2 on a new line, then save the file.

3. Create a new file simply called ssh in the SD card as well. By default SSH is now disabled so this is required to enable it. Remember - Make sure your file doesn't have an extension (like .txt etc)!

4. Open up the cmdline.txt. Be careful with this file, it is very picky with its formatting! Each parameter is seperated by a single space (it does not use newlines). Insert modules-load=dwc2,g_ether after rootwait. To compare, an edited version of the cmdline.txt file at the time of writing, can be found here.

5. That's it, eject the SD card from your computer, put it in your Raspberry Pi Zero and connect it via USB to your computer. It will take up to 90s to boot up (shorter on subsequent boots). It should then appear as a USB Ethernet device. You can SSH into it using raspberrypi.local as the address.

## Rename host
1. edit /etc/hostname to hid-n-seek

2. Edit /etc/hosts. Change 127.0.1.1 raspberrypi to hid-n-seek

## Enable wifi

1. wpa_passphrase <SSID> <PASSWORD>

2. Paste into /etc/wpa_supplicant/wpa_supplicant.conf

```
country=GB
ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
update_config=1

network={
  <config>
}
```

3. wpa_cli reconfigure
