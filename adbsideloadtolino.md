---
description: Using old Tolino eBook Reader as Display for SignalK
---

# SignalkTolino

* Turning any [Tolino](https://mytolino.de) into a custom App Launcher e.g. for a Fullscreen Display of SignalK Apps

## Free your Book Reader 

### Custom App instalieren - long story short

long story \(german\): [https://www.e-reader-forum.de/t/tolino-vision-2-rooten.147429/](https://www.e-reader-forum.de/t/tolino-vision-2-rooten.147429/)

**short story - \(In my case the regular update kept the fastboot possibility, that's the reason for this shortcut! Try it! If you loose loose fastboot possibility you can downgrade via the build in stock recovery and it's factory reset!**

### Updating the Tolino 

* Download update.zip for your device from [mytolino](https://mytolino.de/software-updates/)
* Copy update.zip on tolino as mass storage to root directory
* reboot tolino will result to a firmware update

### Generating Custom Boot Image with ADB enabled

```text
mkdir custom_boot_image
cd custom_boot_image
unzip ../update.zip
mv boot.img boot.img.orig
abootimg -x boot.img.orig
mv initrd.img initrd.img.orig
mkdir initrd
cd initrd
zcat ../initrd.img.orig | cpio -vid
```

In the file  *default.prop* change `ro.secure=0` to `ro.debuggable=1` and set `persist.sys.usb.config=mass\_storage,adb` Nothing else has to be set, than run:

```text
find . | cpio --create --format='newc' | gzip > ../initrd_adb_enabled.img
 cd ..
abootimg --create boot_adb_enabled.img -f bootimg.cfg -k zImage -r initrd_adb_enabled.img
```

It'll return an error message about the unfitting file size. Take the higher Number and convert it ([online](www.rapidtables.com)) to hexadeicimal and insert it in the bootimg.cfg at file size entry!!!

Now yo can temporary\(!\) mount this boot image with adb via `fastboot boot`

* set Tolino to Fastboot
  * Connect USB from Laptop to tolino
  * turn tolino off
  * keep backlight button pushed
  * also push power button and keep it pushed
  * check fastboot connection: `fastboot devices`

    ```text
    fastboot boot boot_adb_enabled.img
    ```

    Tolino should boot regularly with adb enabled check it via `adb devices`

get [F-droid.apk](https://f-droid.org) and [reLaunchX.apk](https://f-droid.org/de/packages/com.gacode.relaunchx/)

Sideload install the two via:

```text
adb install f-droid.apk
adb install com.gacode.relaunchx.apk # filename may vary
```

If you get error maybe you need to restart adb as root:

```text
adb kill-server
sudo adb start-server
```

* Now you can simply restart the tolino and It'll boot to stock

* Choose ReLaunchX as custom Launcher, when asked on first startup \(You can move to Tolino Launcher/Menu any time by choosing it in relaunchX App Menu\)

* You can install apps without actually rooting the tolino via f-droid

* You can go to ReLaunchX Applauncher and go to android settings and go to developer option to temporary activate ADB for sideload operations...

**Having the full power of [F-Droid](https://f-droid.org) and pure .apk Installation you can install [lightning Browser form F-Droid](https://f-droid.org/de/packages/acr.browser.lightning/) that gives you nice fullscreen view and you can choose your favorite Way of Displaying SignalK Values. More Details [here](https://github.com/koileLab/SignalkTolino/blob/master/signalk-eink.md)**

### Helpfull Stuff 

**TWRP for Tolino** via [Ryogo-Zs Github](https://github.com/Ryogo-Z/tolino_ntx_6sl_twrp/releases/)

Key combinations for all Tolinos to get in *Recovery* Mode (**not Fastboot**) on [Papierlos Lesen(german)](https://papierlos-lesen.de/faq/wie-laesst-sich-der-tolino-in-den-recoverymodus-versetzen/) 



