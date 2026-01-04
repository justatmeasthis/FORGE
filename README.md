# **FORGE**  
**F**irmware **O**verwrite (and) **R**eflash (for) **G**oogle **E**quipment

https://github.com/justatmeasthis/FORGE/blob/main/ForgeLogo.png

> [!CAUTION]
> WARNING!!!! THIS HAS A CHANCE OF BRICKING IF YOUR DUMB, DO NOT DO THIS UNLESS ITS YOUR OWN DEVICE (NOT THE SCHOOLS) THIS IS FOR EDUCATIONAL PURPOSES ONLY

> [!IMPORTANT]
> Ti50 tutorial coming soon :D

## TL;DR
In summary this erases your bios, then adds a new one set with the gbb flags you choose, letting you boot in SH1MMER via CTRL+U and do ACE.  
## PRE Requisites
Please **dont** use this exploit if the ANY of the following applies to you, this is because there are **far better** exploits  
- KV6≤
- Not keyrolled
- Skid
## Requirements
Check these things to see if you can do this:  
1. CH341A programmer kit.
2. USB w/ SH1MMER.
3. Secondary laptop with Linux & NeoProgrammer installed.
4. Screwdriver.
5. Knowledge on how to open up your chromebook and where the flash chip is.
6. 45+ Watt charger
7. If your GSC is Ti50, please wait for me to upload a tutorial.
  
## TUTORIAL
 Press ESC+⟳+⏻.  
Should show something like this (creds to MercuryWorkshop for these images):  
  
<img src="https://github.com/MercuryWorkshop/sh1mmer/blob/beautifulworld/assets/recover_black.png" alt="Recovery screen"/>
  
 Press CTRL+D and and continue.  
  
Turn off computer after it shows return to secure mode screen. (TONORM)  
  
<img src="https://github.com/MercuryWorkshop/sh1mmer/blob/beautifulworld/assets/confirm_black.png" alt="TONORM"/>
  
 Open up the chasis of the chromebook. (screwdriver required) 
  
**DISCONNECT THE BATTERY**  
> [!TIP]  
> Look at your chip clip and find the red wire, then look at the chip on your computer and look for a circle, this circle points to where PIN 1 is.  
> The red wire = pin 1, make it so the red wire is attached to pin one.  
  
Plug in the ch341a programmer into the Secondary computer and open up NeoProgrammer  
The image below will help you find where each button is.  
  
<img src="https://github.com/justatmeasthis/FORGE/blob/main/NeoCheatsheet.png" alt=NeoCheetsheet/>  
  
@ Click the detect button to see the flash chip, then follow this loop:  
  
- Connecting Error CH341 (Not found): make sure its firmly plugged in dumbo.  
- IC Not Responding: move the chip clip a little bit to make sure its firmly attached.  
- Multiple Chips Showing: unplug your chip clip and look at your flash chip to see the writing on it, take a screenshot of that writing and then search for that writing on the search bar once youve put the chip clip back.
  
Once you get out that loop, DO the bulletin instructions **TWICE**  
  
- Click Read IC  
- (It should take a long time, thats ok)  
- Click Unlock  
- Click Save File (if this is your second loop, rename the second save as BACKUP)
  
 On your linux terminal, then type ``diff /path/to/file.bin /path/to/BACKUPfile.bin``  
  
 If theres no output, good! If there is an output, delete the 2 files and go back to the step w/ the @ symbol.  
  
**DO NOT TOUCH THE CHIP CLIP FROM NOW ON**  
  
 Download the [gbb_utility](https://github.com/justatmeasthis/FORGE/raw/refs/heads/main/gbb_utility) attached to this git (creds to [mrchromebox](https://mrchromebox.tech), ty :D)  
  
 Do ``./path/to/gbb_utility /path/to/file.bin --set --flags=0x8091`` on your linux terminal (you can replace 0x8091 with whatever you want, but it MUST have DISABLE_FWMP)  
  
 On the NeoProgrammer, press the open file button, then press on file.bin (NOT backupfile.bin)  
  
 Press Erase IC
(It should take a long time, thats ok)  
  
Press Write IC  
  
You did it! you wrote GBB flags while still being enrolled! You may now remove the chip clip and THEN plug in your charger
  
> [!IMPORTANT]
> If your device isnt Booting despite a charger bein plugged in after a minute, your bios might be corrupted, goto [CorruptBiosCR50.md](https://github.com/justatmeasthis/FORGE/blob/main/CorruptBiosCR50.md) for more info.
  
! Using the external disk option (CTRL+U) goto sh1mmer and in the bash shell do ``vpd -l`` and take a screenshot of the output, this is for once you decide to re enroll.  
  
Make sure to type EVERYTHING exactly as they are shown.  
  
``vpd -i RO_VPD -s stable_device_secret_DO_NOT_SHARE="$(openssl rand -hex 32)"``  
``vpd -i RO_VPD -s serial_number="RANDSERIALHERE1234"``  
``vpd -i RW_VPD -s block_devmode="0"``  
``vpd -i RW_VPD -s check_enrollment="0"``  
``crossystem block_devmode=0``  
``reboot -f``  
To Re-enroll, check the [ReEnroll.md](https://github.com/justatmeasthis/FORGE/blob/main/ReEnroll.md)  
