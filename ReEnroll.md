# ReEnrolling
> [!IMPORTANT]
> This will make you keep your GBB flags, making unenrollment easier.
## TL;DR
We will change our S/N as well as device secret back to what it was as well as do calignosity.
## TUTORIAL
Go in your shim via CTRL+U  
  
Open bash terminal  
  
Look for the screenshot you took when you typed ``vpd-l``  
  
Type in the following:  
``vpd -i RW_VPD -s check_enrollment=1 -s block_devmode=1``  
``crossystem block_devmode=1``  
``crossystem dev_boot_usb=0``  
``crossystem disable_dev_request=1``  
``vpd -i RO_VPD -s serial_number="OriginalS/N" -s stable_device_secret_DO_NOT_SHARE="Originaldevicesecret"``  
``reboot -f``  
  
Press return to secure mode (To not get flagged by GAC)  
  
## Returning back to unenrollment
To unenroll again, go back the the README.md and skip to the line w/ the exclamation mark at the beginning.
