# Grinn LCD Example

This repository contains various examples for [Buildroot][Buildroot] and [liteSOM][liteSOM]
device produced by [Grinn sp. z o.o.][Grinn]

## How to setup project with Grinn examples?

### Download and extract Buildroot release, for example

    wget https://buildroot.org/downloads/buildroot-2019.08.tar.gz
    tar xf buildroot-2019.08.tar.gz

### Clone this repository

    git clone https://github.com/DannyKerstens/Grinn_LCD.git
### Apply patch

    Add the 0004-Fix-ILI2117support-ili210x.patch file to the folder path: Buildroot-2019.08/package/patch.
### Configure buildroot to use customizations from this repository

    cd buildroot-2019.08
    make BR2_EXTERNAL=/tmp/Grinn_LCD list-defconfigs

where `/tmp/Grinn_LCD` should point to the repository cloned in the 2nd step.

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

When the build is finished you can load the build on a sd card.

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

## External links

* Grinn home page: http://grinn-global.com
* Grinn wiki: https://wiki.grinn-global.com
* chiliSOM platform: http://chilisom.com
* liteSOM platform: http://litesom.com

[Grinn examples]: https://github.com/grinn-pub/examples.git
[liteSOM]: http://litesom.com/
[Buildroot]: https://buildroot.org/
[Grinn]: http://grinn-global.com/
