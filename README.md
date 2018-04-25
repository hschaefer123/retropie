# RetroPie
Welcome to my custom RetroPie build using a lot of classic old school roms and preconfigured to be used on 16:9 lcd tv with HDMI plug.
### What is RetroPie?
> [RetroPie](https://retropie.org.uk/) allows you to turn your Raspberry Pi, ODroid C1/C2, or PC into a retro-gaming machine. It builds upon Raspbian, EmulationStation, RetroArch and many other projects to enable you to play your favourite Arcade, home-console, and classic PC games with the minimum set-up. For power users it also provides a large variety of configuration tools to customise the system as you want.

Welcome to my [RetroPie](https://retropie.org.uk/) install doc.
This doc describes the setup tasks for my custom [RetroPie 4.4](https://retropie.org.uk/docs/First-Installation/) version.

## Prerequisites
This version is prebuilt for the following hardware spec:
(You can save extra costs by using cheaper case and cable based controller).

Hardware | Shop | Price
-------- | :----: | -----:
Raspberry Pi 3 Model B+|[Amazon](https://www.amazon.de/gp/product/B07BDR5PDW/ref=as_li_qf_asin_il_tl?ie=UTF8&tag=hschaefer123-21&creative=6742&linkCode=as2&creativeASIN=B07BDR5PDW&linkId=94b9bf3e7bd8c40389f7d453d608c300)|EUR 37,90
Rydges EU 5V 3A Micro USB Stecker Netzteil|[Amazon](https://www.amazon.de/gp/product/B01E75SB2C/ref=as_li_qf_asin_il_tl?ie=UTF8&tag=hschaefer123-21&creative=6742&linkCode=as2&creativeASIN=B01E75SB2C&linkId=ba5bdc36e3781015904f5402cf292130)|EUR 9,29
SanDisk Ultra 64GB microSDXC (see [compatible](https://elinux.org/RPi_SD_cards) cards)|[Amazon](https://www.amazon.de/gp/search/ref=as_li_qf_sp_sr_il_tl?ie=UTF8&tag=hschaefer123-21&keywords=SanDisk%20Ultra%2064GB%20microSDXC%20Speicherkarte&index=aps&camp=1638&creative=6742&linkCode=xm2&linkId=18f6ce49891199384a6f2a17caad77f2)|EUR 22,49
Retroflag NESPi CASE+ (NESPi Case PLUS can have SAFE SHUTDOWN and SAFE RESET functions) |[Amazon](https://www.amazon.de/gp/product/B07CG4TR2P/ref=ox_sc_act_title_1?smid=A2Z5GDGNMQA8Q1&psc=1)|EUR 26,99
8Bitdo N30 Pro Wireless Gamepad Controller|[Amazon](https://www.amazon.de/8Bitdo-Wireless-Gamepad-Controller-Android/dp/B013B61SCS/ref=sr_1_3?s=computers&ie=UTF8&qid=1518366736&sr=1-3&keywords=8bitdo)|EUR 34,40
HDMI cable or 4 Pole RCA to 3.5mm Cable (HDMI works best)|[Amazon](https://www.amazon.de/AmazonBasics-Hochgeschwindigkeits-HDMI-Kabel-Ethernet-4K-Videowiedergabe-1-8m-Schwarz/dp/B014I8SSD0/ref=sr_1_1?s=ce-de&ie=UTF8&qid=1518367593&sr=1-1&keywords=hdmi%20cable)|EUR 7,99
**Total**||**EUR ~135,00**

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
Downgrade pi-bluetooth from 0.1.1 back to version 0.1.0
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
## Controller
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

## Transferring Roms
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
