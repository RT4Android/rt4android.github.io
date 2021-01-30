---
layout: other
---

# Restore Windows Phone 8 (Windows instructions)
_____________
### Thanks to <a href="https://forum.xda-developers.com/member.php?u=7887107">trashmaster76</a> and <a href="https://github.com/feherneoh">feherneoh</a>. 
<a href="https://forum.xda-developers.com/nokia-lumia-520/development/restore-windows-phone-8-installed-t3608223" class="btn2">Go to XDA Thread</a>

> DO NOT ask for a backup. If you do not have one, you have to accept to be permanently on Android.


**1)** Download this zip and extract it in a new folder:

<a href="https://github.com/Android4Lumia/android4lumia.github.io/raw/master/files/WP_Restore.zip" class="btn2">WP_Restore.zip</a>

**2)** Copy the backup to that folder. Create another folder inside this one called "**parts**".

**3)** Open CMD in the folder that you created in step 1 and run this command: 

```imgman64.exe backup.img parts```

(Replace **backup.img** with the filename of your backup)

**4)** Now, run these commands:

```
fastboot boot recovery_unsecure.img
adb push fame_wp_unlocked.gpt /cache/
adb shell
sgdisk --load-backup /cache/fame_wp_unlocked.gpt /dev/block/mmcblk0
sync
sync
reboot
```

Phone will reboot. ADB should disconnect at this point.

**5)** Now we have to flash every partition that is in the parts folder with this command:

```
fastboot flash partition parts\partition.img
```

Change **partition** with one of these (**flash them in this order!**):

* TZ
* SSD
* RPM
* WINSECAPP
* MODEM_FSG
* MODEM_FS1
* MODEM_FS2
* UEFI_BS_NV
* UEFI_NV
* UEFI_RT_NV
* UEFI_RT_NV_RPMB
* PLAT
* MMOS
* EFIESP
* UEFI

**6)** Reboot the phone with ```fastboot reboot```

Phone will now show smiley of death, that is normal.

At this point, you can use Windows Device Recovery Tool to flash a clean Windows Phone or reflash the one from the backup using thor2.

## How to flash Windows Phone FFU with thor2
___________________
**Note:** Instead of thor2 you can flash FFU with Windows Phone Internals or Windows Device Recovery Tool.

thor2 should be at:

64 Bits Windows: ```C:\Program Files (x86)\Microsoft Care Suite\Windows Device Recovery Tool```

32 Bits Windows: ```C:\Program Files\Microsoft Care Suite\Windows Device Recovery Tool```

**1)** Go to the thor2 folder and open CMD in it.

**2)** Run this command: ```thor2 -mode rnd -bootflashapp```

**3)** Flash your phone's FFU file (download from <a href="https://lumiafirmware.com/">LumiaFirmware</a>) with:

```thor2 -mode uefiflash -ffufile <Path-to-FFU> -do_full_nvi_update -do_factory_reset```

**4)** Reboot your phone with ```thor2 -mode rnd -bootnormalmode```

Done! Windows Phone 8 should boot.
