# **FORGE**
**F**irmware **O**verwrite (and) **R**euse (for) **G**oogle **E**quipment
WARNING!!!! THIS HAS A CHANCE OF BRICKING IF YOUR DUMB, DO NOT DO THIS UNLESS ITS YOUR OWN DEVICE (NOT THE SCHOOLS)
In summary this erases your bios, then adds a new one set with the gbb flags you choose, letting you boot in SH1MMER via external disk, and changes the device secret as well as the S/N.
Check these things to see if you can do this:
1. CH341A programmer kit
2. USB
3. Knowledge on how to open **your** chromebook, and location of **your** flash chip
4. A charger
5. Secondary computer with linux and NeoProgrammer installed
6. Not being a skid
7. Common sense
8. A brain
9. Being smart
10. I just wanna see this reach to 10 :D \n
With that out of the way, lets begin!\n
Turn off the chromebook, Flip it to the back with the screws and stuff, and open the back to access the lovely PCB.\n
**DISCONNECT THE BATTERY**
Look at your chip clip and find the red wire, then look at the chip on your computer then look for a circle, this circle points to where PIN 1 is.
The red wire = pin 1, make it so the red wire is attached to pin one.
then plug in the ch341a programmer into the computer with linux and NeoProgrammer installed
**note for me, change the instructions below as the order may not be accurate**
- open up NeoProgrammer, click the detect button to see the flash chip, then follow this loop
  Connecting error CH341 (Not found): make sure its firmly plugged in dumbo
  IC not responding? move the chip clip a little bit to make sure its firmly attached
  Multiple Chips showing? unplug your chip clip and look at your flash chip to see the writing on it, take a screenshot of that writing and then search for that writing on the search bar once youve put the chip clip back.
Once you get out that loop, DO THIS **TWICE**
  Click read IC
  (It should take a long time, thats ok)
  Click Unprotect
  Click save (if this is your second loop, rename the second save as BACKUP)
Goto your linux terminal, then type ``diff /path/to/file.bin /path/to/BACKUPfile.bin``
If theres no output, good! if there is an output, go back up to the instruction that starts with a hyphen.
**KEEP THE CHIP CLIP ON FROM NOW ON**
Download the gbb_utility attached to this git (creds to mrchromebox, ty :D)
Do ``./path/to/gbb_utility /path/to/file.bin --set --flags=0x8091`` on your linux terminal (you can replace 0x8091 with whatever you want, but it MUST have DISABLE_FWMP)
Back to the NeoProgrammer press the open file button, then press on file.bin (NOT backupfile.bin)
Press erase IC
(It should take a long time, thats ok)
Press write IC
You did it! you wrote GBB flags while still being enrolled! Now check if you have a USB. If you dont, thats fine!
If you have a usb, goto sh1mmer and in the bash shell do ``vpd -l`` and take a screenshot of the output, this is for once you decide to re enroll.
Make sure to type EVERYTHING exactly as they are shown.
Type ``vpd -i RO_VPD -s stable_device_secret_DO_NOT_SHARE="$(openssl rand -hex 32)"``
Type ``vpd -i RO_VPD -s serial_number="TYPERANDOMSERIALHERE1234"``
Type ``vpd -i RW_VPD -s block_devmode="0"``
Type ``vpd -i RW_VPD -s check_enrollment="0"``
Type ``crossystem block_devmode=0``
You are now unenrolled, yippee!!
