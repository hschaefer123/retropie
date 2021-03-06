# RetroPie
Welcome to my custom [RetroPie](https://retropie.org.uk/) build using a lot of classic old school roms and preconfigured to be used on 16:9 lcd tv with HDMI plug. This doc describes my used tasks following the [RetroPie 4.4](https://retropie.org.uk/docs/First-Installation/) first installation guide.
### What is RetroPie?
> [RetroPie](https://retropie.org.uk/) allows you to turn your Raspberry Pi, ODroid C1/C2, or PC into a retro-gaming machine. It builds upon Raspbian, EmulationStation, RetroArch and many other projects to enable you to play your favourite Arcade, home-console, and classic PC games with the minimum set-up. For power users it also provides a large variety of configuration tools to customise the system as you want.
## Prerequisites
This version is prebuilt to be used with the following hardware specification:<br>
(You can save extra costs by using a cheaper case and a cable based controller).

Hardware | Shop | Price
-------- | :----: | -----:
Raspberry Pi 3 Model B+|[Amazon](https://www.amazon.de/dp/B07BDR5PDW/?coliid=I1V8JD1IG8PU09&colid=DSIE50YYL8VQ&psc=0&ref_=lv_ov_lig_dp_it)|EUR 37,90
Heat sink for Raspberry Pi 3|[Amazon](https://www.amazon.de/dp/B01CP4JRPW/?coliid=I1HH1ERRNJVIW2&colid=DSIE50YYL8VQ&psc=0&ref_=lv_ov_lig_dp_it)|EUR 6,90
Rydges EU 5V 3A Micro USB Stecker Netzteil :electric_plug:|[Amazon](https://www.amazon.de/dp/B01E75SB2C/?coliid=I33IZFZ4VJGG39&colid=DSIE50YYL8VQ&psc=0&ref_=lv_ov_lig_dp_it)|EUR 9,29
SanDisk Ultra 64GB microSDXC (see [compatible](https://elinux.org/RPi_SD_cards) cards)<br>[Samsung EVO Plus Micro SDXC 64GB] (alternative)|[Amazon](https://www.amazon.de/dp/B073SB2L3C/?coliid=I25R2PLO9M1NJ3&colid=DSIE50YYL8VQ&psc=0&ref_=lv_ov_lig_dp_it)<br>[Amazon](https://www.amazon.de/dp/B06XFZV9JY/?coliid=I254Y8MA9PGHVW&colid=DSIE50YYL8VQ&psc=0&ref_=lv_ov_lig_dp_it)|EUR 22,49<br>[EUR 21,78]
[Retroflag](http://retroflag.com/) NESPi CASE+ (NESPi Case PLUS can have SAFE SHUTDOWN and SAFE RESET functions) |[Amazon](https://www.amazon.de/dp/B07CG4TR2P/?coliid=IAULN9J8Y04WQ&colid=DSIE50YYL8VQ&psc=0&ref_=lv_ov_lig_dp_it)|EUR 26,99
[8Bitdo N30 Pro](http://www.8bitdo.com/n30pro-f30pro/) Wireless Gamepad Controller|[Amazon](https://www.amazon.de/dp/B013B61SCS/?coliid=I1UMG7SWQKD1OH&colid=DSIE50YYL8VQ&psc=0&ref_=lv_ov_lig_dp_it)|EUR 34,40
HDMI cable or 4 Pole RCA to 3.5mm Cable (HDMI works best) :tv:|[Amazon](https://www.amazon.de/dp/B014I8SSD0/?coliid=I2N0A32S168KF9&colid=DSIE50YYL8VQ&psc=0&ref_=lv_ov_lig_dp_it)|EUR 7,99
**Total** (prices are changing hourly)|:de: :link:|**EUR ~150,00**

# Install
## Enable SSH
**Note**: Starting with RetroPie 4.2, in order to keep the default image secure SSH is disabled by default. Press F4 to leave Emulation Station Menu to console. Re-enable SSH in raspi-config:
```
sudo raspi-config
```
Interfacing Options >> SSH >> Enable >> reboot your pi
```
sudo reboot
```
### Default Login:
username: **pi**
password: **raspberry**
### Common Terminal Commands:
**Reboot:**
```
sudo reboot
```
**Shutdown:**
```
sudo shutdown -h now
```
**Change Directory:**
```
cd /path/to/directory
```
**list Files in Current Directory:**
```
ls
```
**Retropie Setup Script:**
```
sudo /home/pi/RetroPie-Setup/retropie_setup.sh
```
**Start Emulation Station:**
```
emulationstation
```
## Bluetooth Downgrade
RetroPie currently has issues using Bluetooth Version 1.1, therefore a downgrade for pi-bluetooth from 0.1.1 back to version 0.1.0 is nessesary!
```
wget http://archive.raspberrypi.org/debian/pool/main/p/pi-bluetooth/pi-bluetooth_0.1.0_armhf.deb
sudo dpkg -i pi-bluetooth_0.1.0_armhf.deb
```
## Overlays
Install Arcade game overlays created for Lr-Mame2003 from UDb23 (latest version with correct aspect ratio) and 1080p Display.
```
cd
git clone --depth 1 https://github.com/meleu/rpie-art
cd rpie-art
./rpie-art.sh
```
## Controller :video_game:
Make sure, that you are using the latest [Firmware v4.10](http://download.8bitdo.com/Firmware/Controller/N30pro+F30pro/N30pro+F30pro_Firmware_V4.10.zip) to be able to disable hack.
Add and configure 8bitdo bluetooth controller as described [here](https://retropie.org.uk/docs/8Bitdo-Controller/). 

 1. Run retropie-setup script (see SSH)
 2. Choose the "Configuration / Tools" menu choice
 3. Choose the "bluetooth - Configure Bluetooth Devices" menu choice 
 4. Make sure the hack option is turned "off"
 5. Make sure your controller is powered on and searching for a connection. With the FC30 Pro, this is done by holding the power button (left-hand side of the base of the controller) on until the side blue lights illuminate.
 6. Choose the "Register and Connect to Bluetooth Device" 
 7. You will then see the "Searching" screen. If you have issues with the detection of the controller, you may find it helps to press some buttons on the controller when this screen is showing. 
 8. It may be the case that the first time the results are returned, the name of the controller doesn't show, or that the MAC address doesn't show at all. If that's the case, you can either select the device if you know the MAC or simply search again.
 9. Choose the "DisplayYesNo" optin to complete the registration process.
 10. You must now setup the udev rule in order for Emulation Station to "see" the controller when you restart your Raspberry Pi.

```
sudo reboot
```
Configure Controller, use SELECT as HOTKEY
## NESPi CASE PLUS
Install [Safe Shutdown and Safe Reset](https://github.com/RetroFlag/retroflag-picase) script for [retroflag](http://retroflag.com/) case: 
```
wget -O - "https://raw.githubusercontent.com/RetroFlag/retroflag-picase/master/install.sh" | sudo bash
```
 ## Emulation Station
 ### Scraper
> Scraping is a way to get metadata and boxart for your games from the internet. The scrapers RetroPie uses pull primarily from thegamesdb.net
 
 Scrapping Videos
 
 - Update RetroPie-Setup script
 - Manage Packages >>> Manage optional packages >>> scraper >>> Install from source
 - Configuration options
	 - Thumbnails only (Disabled)
	 - Arcade Sources (ArcadeItalia)
	 - Console Source (ScreenScraper)
	 - ROM Names (theGamesDB)
	 - Gamelist (Overwrite)
	 - Use rom folder for gamelist & images (Enabled)
	 - Download Videos (Enabled)
	 - Download Marquees (Enabled)

 - Emulation Station Menu
	 - UI Settings
		 - Gamelist View Style -> VIDEO
	 - Other Settings
		 - Use OMX Player (HW Accelerated) -> ON

## Transferring Roms :space_invader:
The following roms are used in the custom build

Folder|Emulator|Options|Games
---|---|---|---:
atari2600|Atari 2600|Config Editor use Analog Stick|607
atari7800|Atari 7800|Europe Set|55|
atarilynx|Lynx||76|
daphne|Daphne|Install optional package 'daphne'||
fds|Family Computer Disk System||91|
gamegear|Game Gear||250|
gb|Game Boy||585|
gbc|Game Boy Color||543|
genesis|Genesis||
intellivision|Intellivision|Install optional package 'jzintv'|141|
mame-libreto|MAME 2003|Config Editor use Analog Stick|4691
mastersystem|SEGA Master System||286
megadrive|SEGA Mega Drive||816
nds|Nintendo DS||
neogeo|NEO GEO||141
nes|Nintendo Entertainment System||906
pcengine|PC Engine (TurboGrafx-16)||104
sega32x|SEGA 32X||33
sg-1000|SG-1000||68
snes|Super Nintendo Entertainment System||821
vectrex|Vectrex||25
wonderswan|Wonderswan Color|Install optional package 'lr-beetle-wswan'|109
wonderswancolor|WonderSwan|Install optional package 'lr-beetle-wswan'|91
