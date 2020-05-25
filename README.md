# Grinn LCD Example

This repository contains various examples for [Buildroot][Buildroot] and [liteSOM][liteSOM]
device produced by [Grinn sp. z o.o.][Grinn] edited for Skalar purposes.

## How to setup project with Grinn examples?

### Download and extract Buildroot release, for example

    wget https://buildroot.org/downloads/buildroot-2019.08.tar.gz
    tar xf buildroot-2019.08.tar.gz

### Clone this repository

    git clone https://github.com/DannyKerstens/Grinn_LCD.git

### Configure buildroot to use customizations from this repository

    cd buildroot-2019.08
    make BR2_EXTERNAL=/tmp/Grinn_LCD list-defconfigs

where `/tmp/Grinn_LCD` should point to the repository cloned in the 2nd step.(example: /home/<username>/Grinn_LCD)

Target `list-defconfigs` shows list of available _defconfigs_. After _built-in configs_ you 
should see configs provided by the external customizations (like [Grinn examples][Grinn examples]).


    make BR2_EXTERNAL=/tmp/examples list-defconfigs
    Built-in configs:
      acmesystems_aria_g25_128mb_defconfig - Build for acmesystems_aria_g25_128mb
      acmesystems_aria_g25_256mb_defconfig - Build for acmesystems_aria_g25_256mb
      [...]
      
    External configs in "Grinn examples":
      grinn_liteboard_can_defconfig       - Build for grinn_liteboard_can
      grinn_liteboard_lcd_res_defconfig   - Build for grinn_liteboard_lcd_res
      grinn_liteboard_spi_defconfig       - Build for grinn_liteboard_spi
      grinn_liteboard_telit_defconfig     - Build for grinn_liteboard_telit


### Configure build configuration, for example

    make grinn_liteboard_lcd_res_defconfig
    
### Build software

    make all

When the build is finished you can load the build on a sd card. be adviced this can take some time based on your computer.

	sudo dd if=output/images/sdcard.img of=/dev/<SD-CARD> bs=4M
	
<SD-CARD> Should point to the location of your sd card. You can find the location with:

	lsblk

It should look something like this:

	NAME                      MAJ:MIN RM   SIZE RO TYPE MOUNTPOINT
	sda                         8:0    0 238.5G  0 disk 
	├─sda1                      8:1    0    28G  0 part /
	├─sda2                      8:2    0     1K  0 part 
	├─sda5                      8:5    0   9.3G  0 part 
	└─sda6                      8:6    0 201.2G  0 part /home
	sr0                        11:0    1  1024M  0 rom  
	mmcblk0                   179:0    0  14.7G  0 disk 
	└─mmcblk0p1               179:1    0  14.7G  0 part /media/foo/804b0b54

In this case the sd card is located at mmcblk0. In most cases it is located under sdb.

for information on loading the image on the internal memory i refer to the following tutorial:

https://wiki.grinn-global.com/doku.php?id=litesom:buildroot:qa

### Debugging

For the debugging of the litesom you will have to connect the board with a micro USB cable to your desktop. Open a serial port with an application like PuTTY. check wich com port to use and set the baud rate to 115200.

![serial](https://user-images.githubusercontent.com/64635066/82794269-7be09e80-9e72-11ea-9be9-8049fc9e89f4.PNG)

If you did everything correctly you wil have a startup log of the litesom on PuTTY. At the end of the log it will ask for a password. By default this password is root.

![Capture](https://user-images.githubusercontent.com/64635066/82794593-00cbb800-9e73-11ea-86dc-4dd3507c1167.PNG)

Once your logged in you can find some test application in the folder /usr/bin.
## External links

* Grinn home page: http://grinn-global.com
* Grinn wiki: https://wiki.grinn-global.com
* chiliSOM platform: http://chilisom.com
* liteSOM platform: http://litesom.com

[Grinn examples]: https://github.com/grinn-pub/examples.git
[liteSOM]: http://litesom.com/
[Buildroot]: https://buildroot.org/
[Grinn]: http://grinn-global.com/
