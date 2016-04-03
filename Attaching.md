# Attaching Hard Disk Drives #

A hard disk drive has to be attached RAW CCTV Replay by an [admin user](Running#UserLevels.md) before it can be viewed. It is recommended that the hard disk drive is attached via a physical write blocking device. With the hard disk drive attached to the server computer, the admin user attaches it via the web interface. Once [logged in](WebInterface.md), the "Configure Disks" option is found under "Menu".

![http://raw-cctv-replay.googlecode.com/files/raw_activate_disk_menu_v1_0.jpg](http://raw-cctv-replay.googlecode.com/files/raw_activate_disk_menu_v1_0.jpg)

This brings up the "Manage active video sources" screen which lists all the attached hard disk drives (other than those that were indicated in the configuration file to be ignored).

![http://raw-cctv-replay.googlecode.com/files/raw_activate_disk_screen_v1_0.jpg](http://raw-cctv-replay.googlecode.com/files/raw_activate_disk_screen_v1_0.jpg)

For each hard disk drive, the user can enter a case identification number and the results of the time and date check when the hard drive was seized. The latter is used to estimate real time upon replay. The user then selects the appropriate module from the drop down list and presses the "Activate module" button.

The program then accesses the hard disk drive to establish that it is indeed of the format selected and establishes what video is present. When this process is complete (which may take some time depending upon the amount of data on the hard disk drive and the format) the module is activated for that hard disk drive.

![http://raw-cctv-replay.googlecode.com/files/raw_activated_module_v1_0.jpg](http://raw-cctv-replay.googlecode.com/files/raw_activated_module_v1_0.jpg)

The hard disk is then ready for [viewing](Viewing.md).
