Some instructions on how to do a "manual update" of Lenovo Thinkpad BIOS/UEFI (for example if your laptop has a dead battery, as Lenovo's frontend tool requires a >50% charged battery)

# Before you start...
Here we will use the `winflash64.exe` tool provided directly by Lenovo and written by Phoenix Technolgies (this exe is included with the installers from Lenovo's website). 
Personally I haven't had much luck with the PhoneixUEFI flasher tool so I don't really recommend you use it...
(In fact the normal tool is just a frontend wrapper around `winflash64.exe`, so by calling this tool directly from the command line we can bypass the battery checks Lenovo has put in).
Run `winflash64.exe -help` to display all the options.

# Firstly...
Go to Lenovo's website and download the BIOS updater installer for Windows for your machine.
Install it and go to the directory where the files are extracted (e.g. C:\DRIVERS\FLASH\n25uj25w)
Now go into the folder containing the BIOS files (this usually follows the name of the BIOS given in the txt instructions on Lenovo's website, e.g. N25ET49W)
There may be one or two FL files in this folder along with a couple of XML files -- we only care about the FL files. Separate instructions are below depending on the contents of this folder. 

## If your laptop has only ONE `.FL1` file (eg Thinkpad Edge E431/E531, Yoga S1, Yoga 12)
This means that the BIOS/UEFI and EC are combined into the same file.
Copy the `.FL1` file into the parent directory (containing `winflash64.exe`)
