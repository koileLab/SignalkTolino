---
description: Using old Tolino eBook Reader as Display for SignalK
---

# readme.md

## eBook Reader

* Turning any Tolino
* \*\*\*\*
* **RelaunchX** AppLauncher & Filebrowser für Tolino aus F-Droid [https://f-droid.org/en/packages/com.gacode.relaunchx/](https://f-droid.org/en/packages/com.gacode.relaunchx/)
* Kompatibilität von [https://github.com/ieb/sailinstruments/https://github.com/ieb/sailinstruments/](https://github.com/ieb/sailinstruments/https://github.com/ieb/sailinstruments/) mit Tolino prüfen
* Alternative E-Ink App in SignalK [https://github.com/ieb/signalk-eink](https://github.com/ieb/signalk-eink)

#### Custom App instalieren - long story short

long story \(german\): [https://www.e-reader-forum.de/t/tolino-vision-2-rooten.147429/](https://www.e-reader-forum.de/t/tolino-vision-2-rooten.147429/)

**short story - \(In my case the regular update keept the fastboot possibility, that's the reasion for this shortcut! Try it! If you loose loose fastboot possibility you can downgrade via the build in stock recovery and it's factory reset!\)**

* Download update.zip for your device from [mytolino](https://mytolino.de/software-updates/)
* Copy update.zip on tolino as mass storrage to root 
* reboot tolino will resault fw update

Making Custom Boot Image with ADB enabled

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

Auch hier wieder in der Datei default.prop "ro.secure=0", "ro.debuggable=1" und "persist.sys.usb.config=mass\_storage,adb" setzen. Ansonsten muss nichts weiter angepasst werden. Code:

```text
find . | cpio --create --format='newc' | gzip > ../initrd_adb_enabled.img
 cd ..
abootimg --create boot_adb_enabled.img -f bootimg.cfg -k zImage -r initrd_adb_enabled.img
```

It'l return an errormessage about unfitting filesize. Take the higher Number and convert it to hexadeicimal and insert it in the bootimg.cfg at filesize entry!!!

Now yo can temporarly\(!\) mount this boot image with adb via `fastboot boot`

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

Sideload install both via:

```text
adb install f-droid.apk
adb install com.gacode.relaunchx.apk # filename may vary
```

maybe you need to restart adb as root - if you get error

```text
adb kill-server
sudo adb start-server
```

* Now you can simply restart the tolino and It'l boot to stock
* Choose ReLaunchX as custom Launcher, when asked on first startup \(You can move to Tolino Launcher/Menu any time by choosing it in relaunchX App Menu\)
* You can install apps without actually rooting the tolino via f-droid
* You can go to ReLaunchX Applauncher and go to android settings and go to developer option to temporarly activate ADB for sideload operations...

#### TWRP für Tolino via [https://github.com/Ryogo-Z/tolino\_ntx\_6sl\_twrp/releases/](https://github.com/Ryogo-Z/tolino_ntx_6sl_twrp/releases/)

Tastenkombis für alle Tolino Version für Recovery \(!\) nicht fastboot... [https://papierlos-lesen.de/faq/wie-laesst-sich-der-tolino-in-den-recoverymodus-versetzen/](https://papierlos-lesen.de/faq/wie-laesst-sich-der-tolino-in-den-recoverymodus-versetzen/)

* Tolino in den Fastoot Modus versetzen \(Bei angeschlossenem USB ausschalten, Beleuchtungsknopf gedruckt halten, 
* fastboot device \#Check Fasstboot cpowerknopf zusaetzlich gedrueckt halten\)

  onnectivity `fastboot devices` should return a long random value

* fastboot boot twrp.img \# use "boot" so you don't flash TWRP you only use it temporaly

#### SignalK App

* Basierend auf: [https://www.npmjs.com/package/@digitalyacht/sk-on-kindle](https://www.npmjs.com/package/@digitalyacht/sk-on-kindle) hat [https://projekt-kiri.blogspot.com/2018/12/loch-allmahlich-wird-es-zeit-kiri.html](https://projekt-kiri.blogspot.com/2018/12/loch-allmahlich-wird-es-zeit-kiri.html) eine Anpassung gemacht. In dem Kommentaren findet sich der Link zu seiner Dropbox mit dem Code: [https://www.dropbox.com/s/pfmssxxjzkpzd5b/kindle.zip?dl=0](https://www.dropbox.com/s/pfmssxxjzkpzd5b/kindle.zip?dl=0)

  [https://projekt-kiri.blogspot.com/2018/12/loch-allmahlich-wird-es-zeit-kiri.html](https://projekt-kiri.blogspot.com/2018/12/loch-allmahlich-wird-es-zeit-kiri.html)

  Video: [https://diode.zone/videos/watch/b4ac9ba3-72aa-4756-ad32-c580ba9d221c](https://diode.zone/videos/watch/b4ac9ba3-72aa-4756-ad32-c580ba9d221c)



