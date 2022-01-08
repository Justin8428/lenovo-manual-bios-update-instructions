Some instructions on how to do a "manual update" of Lenovo Thinkpad BIOS/UEFI (for example if your laptop has a dead battery, as Lenovo's frontend tool requires a >50% charged battery)

# Before you start...
Here we will use the `winflash64.exe` tool provided directly by Lenovo and written by Phoenix Technolgies (this exe is included with the installers from Lenovo's website). 
Personally I haven't had much luck with the PhoneixUEFI flasher tool so I don't really recommend you use it...
(In fact the normal tool is just a frontend wrapper around `winflash64.exe`, so by calling this tool directly from the command line we can bypass the battery checks Lenovo has put in).
Also note that burning Lenovo's `.iso` file onto a CD or USB will NOT let you skip the battery check!

Run `winflash64.exe -help` to display all the options.

# Firstly...
 - Plug the AC adapter into your machine (and ideally into a UPS if you have one)
 - Go to Lenovo's website and download the BIOS updater installer for Windows for your machine.
 - Install it and go to the directory where the files are extracted (e.g. C:\DRIVERS\FLASH\n25uj25w)
 - Now go into the folder containing the BIOS files (this usually follows the name of the BIOS given in the txt instructions on Lenovo's website, e.g. N25ET49W)
 - There may be one or two FL files in this folder along with a couple of XML files -- we only care about the FL files. Separate instructions are below depending on the contents of this folder. 

## If your laptop has only ONE `.FL1` file (eg Thinkpad Edge E431/E531, Yoga S1, Yoga 12)
This means that the BIOS/UEFI and EC are combined into the same file.

 - Copy the `.FL1` file into the parent directory (containing `winflash64.exe`)
 - Open an adminstrator command prompt and navigate to that directory
 - Run `winflash64.exe /ipf bios ec /file xxx.FL1` (replace `xxx.FL1` with the name of the `.FL1` file)
 - With any luck your machine should reboot in 5 seconds and start the BIOS upgrade process. (It goes without saying that you should not touch the machine while it is updating.) Once it is complete it will automatically reboot into Windows.

Note: if you stuffed up like I did the first time around and forgot to specify the regions to flash (`/ipf` flag) you can repeat the flashing process by issuing the same command, plus an additional `/sd` flag to skip the version check (so e.g. `winflash64.exe /ipf bios ec /file xxx.FL1 /sd`)

## If your laptop has a `.FL1` AND a `.FL2` file (eg most T or X series Thinkpads) -- untested
The `.FL1` file contains the BIOS and `.FL2` contains the EC firmware.

In theory for more modern machines you should be able to copy the `.FL1` and `.FL2` files to the parent folder and simply run `WinFlash64.exe /file xxx.FL1` (replace `xxx.FL1` with the name of the `.FL1` file) and have it take the next file automatically. 

You can also flash the two files separately (possibly less safe as the system can usually boot even with mismatched BIOS and EC versions), making sure to flash the EC file before the BIOS file:

 - Copy the `.FL2` file into the parent directory (containing `winflash64.exe`)
 - Open admin command prompt and run `winflash64.exe /ipf ec /file xxx.FL2` (replace `xxx.FL2` with the name of the `.FL2` file)
 - System will reboot, flash EC and boot back into Windows
 - Go back to the folder and copy the `.FL1` file into the parent directory
 - Open admin command prompt and run `winflash64.exe /ipf bios /file xxx.FL1` (replace `xxx.FL1` with the name of the `.FL1` file)
 - System will reboot, flash BIOS and boot back into Windows. Then you should be done... hopefullly :-)

# References, further reading
https://www.reddit.com/r/thinkpad/comments/aw5xg2/bios_update_for_thinkpad_yoga_260_fl1_fl2_via/
https://superuser.com/questions/1569417/how-to-update-lenovo-bios-on-a-t460-without-battery
https://www.thinkwiki.org/wiki/BIOS_Upgrade#Updating_without_battery_or_with_dead_battery
https://forums.lenovo.com/t5/Gaming-Laptops/Y540-BIOS-Recovery-Mode-Flash-BIOS-from-USB/m-p/5026109 is a useful thread which allegedly details a way to recover from a corrupted BIOS flash

The first part was tested on a Thinkpad Edge E431 on Windows 8.1. However the 2nd part involving 2 files has not been tested by me -- proceed with caution!!
