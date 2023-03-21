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
Install: "curl -sL https://install.raspap.com | bash"
Visit RaspAP web GUI and start configuring things by typing the ip adress in the browser bar
in raspAP bridge instellen
Toggling bridged AP mode
In the RaspAP web interface, go to Hotspot > Advanced tab, then slide the Bridged AP mode toggle. Save settings then Restart hotspot.
![Dit is de afbeelding van hotspot](https://i.imgur.com/xSHY164.png)
klik op [save settings] en dan op [restart hotspot]
Noteer eveneens welke aanpassingen je aan welke configuratiebestanden je hebt doorgevoerd.
## Eigen scripts en programma's
SSH geactiveerd in sudo raspi-config
Sla je als apparte bestanden op in deze respository.
http://snt-guest/
login:admin
paswordt:snt-guest (geplaatst op vraag van leerkracht)

beginnen aan NAS + leren backup maken 28/2/2023
BACKUP maken met WINDISK23 in windows
INSTALLEREN NAS
sudo apt update
sudo apt upgrade
sudo apt install samba samba-common-bin
SOFTWARE CONNECTIE Installeren
Windows 10 herkent op het netwerk aangesloten apparaten door gebruik te maken van Web Service Discovery. Dit is de vervanger van het verouderde NetBios systeem, dat stilaan uit Windows 10 wordt verwijderd. Samba werkt nog niet met Web Service Discovery, waardoor onze NAS niet altijd in Windows Verkenner wordt weergegeven. Tot het nieuwe Windows Web Service Discovery in Samba is geïntegreerd, kan je de volgende software op uw Raspberry Pi installeren en gebruiken:
a. Download het script (software) met de opdracht:
wget https://raw.githubusercontent.com/christgau/wsdd/master/src/wsdd.py
b. Verplaats het script naar de softwaremap van de Raspberry Pi:
sudo mv wsdd.py /usr/bin/wsdd
c. Dit script is voor Raspian nog steeds een eenvoudig tekstbestand. 
Om dit script als programma te kunnen starten, moeten we het uitvoerrechten geven (eXecutable maken):
sudo chmod +x /usr/bin/wsdd
d. We testen het script door het uit te voeren:
/usr/bin/wsdd
e. Stop het wsdd script met de toetscombinatie Ctrl+C.
f. Tijd om het wsdd script automatisch te starten bij het opstarten van de Raspberry Pi:
f1. Download het systemd startscript:
wget https://raw.githubusercontent.com/christgau/wsdd/master/etc/systemd/wsdd.service
f2. Verplaats het opstartscript naar de map met opstartscripts:
sudo mv wsdd.service /etc/systemd/system/
f3. Test het opstartscript door het te starten:
sudo systemctl start wsdd.service
f4. Dit gaat duidelijk fout. Na een grondig onderzoek van het starscript /etc/systemd/system/wsdd.service bleek al vlug dat het standaard configuratiebestand /etc/default/wsdd ontbreekt. Je kunt dit aanmaken met de opdracht:
sudo touch /etc/default/wsdd
f5. Test het opstartscript opnieuw:
sudo systemctl start wsdd.service
f6. Controleer de meldingen van het opstartscript:
sudo systemctl status wsdd.service
f7. De Raspberry Pi NAS verschijnt terug in de Windows Verkenner Netwerkomgeving.
f8. Nu de test geslaagd is, nemen we het startscript op in het opstartsysteem van Raspian:
sudo systemctl enable wsdd.service 

CONFIGUREREN NAS
a. Nu de USB-stick beschikbaar is, moeten we Samba instellen om er gebruik van te maken:
Open als systeembeheerder het Samba configuratiebestand met een teksteditor.
pi@RPIDanPin:~ $ sudo nano -B /etc/samba/smb.conf
b. Voeg op het einde van het configuratiebestand de volgende sectie toe:
[NAS]
   comment = Network-Attached Storage
   path = /media/pi
   read only = yes
   public = yes
   force user = pi

Foolproof maken
We gebruiken het commando sudo raspi-config
en kiezen volgende opties uit het menu
https://learn.adafruit.com/assets/108774
kies dan P3
https://learn.adafruit.com/assets/108775
De overlay system is dus een soort RAM-Drive die alles tijdelijk opslaat zonder aan het besturingsysteem te raken.
Klik op YES
https://learn.adafruit.com/assets/108776
De bootpartitie Wordt hiermee beveiligd en kan dus niet meer gewijzigd worden
Klik op YES
https://learn.adafruit.com/assets/108777
