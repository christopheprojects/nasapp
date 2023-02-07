# nasapp
## Beschrijving
nas met access point
hostname: *******
## Bronnen
Noteer hier uw inspiratie, hardware en software bronnen.
Interessante Access Point projecten:
A portable WiFI router/NAS/Docker using RaspAP on Raspberry Pi 4 with USB/SSD boot device:
https://techsparx.com/linux-sbc/raspberry-pi/pi4-raspap.html
RaspAP — Simple wireless router setup for Debian-based devices:
https://raspap.com/
## Hardware
Noteer hier welke hardware je gebruikt.
Raspberry Pi 3 Model B
8GB SD-kaart
## Software
Noteer hier welke software je gebruikt

RaspAP 
The high level process for installing RaspAP is:

Burn an SD card (or USB drive) with Raspberry Pi OS (or other supported OS). You should probably use the Lite version - with no GUI support - because this device probably won't be used for a desktop user experience
Use an ethernet cord to connect your Raspberry Pi to your Internet router
Boot the Raspberry Pi from the SD card (or USB drive)
Setup: sudo apt-get update && sudo apt-get full-upgrade -y
REBOOT
Config: sudo raspi-config
REBOOT -- raspi-config will probably demand a reboot
Install: curl -sL https://install.raspap.com | bash
Visit RaspAP web GUI and start configuring things
in raspAP bridge instellen
Toggling bridged AP mode
In the RaspAP web interface, go to Hotspot > Advanced tab, then slide the Bridged AP mode toggle. Save settings then Restart hotspot.
https://i.imgur.com/xSHY164.png

Noteer eveneens welke aanpassingen je aan welke configuratiebestanden je hebt doorgevoerd.
## Eigen scripts en programma's
SSH geactiveerd in sudo raspi-config
Sla je als apparte bestanden op in deze respository.
http://snt-guest/
login:admin
paswordt:snt-guest (geplaatst op vraag van leerkracht)
