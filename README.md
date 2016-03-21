# Android-Stuff

## Replace a privileged system app for debug

With this version of adb (Mac):

    Android Debug Bridge version 1.0.35
    Revision 102d0d1e73de-android

Make /system writable by:

    adb root
    adb remount
    adb disable-verity
    adb reboot

Seems to take a few reboots sometimes before the remount succeeds.

It failed for me on an Ubuntu VM. It didn't understand the `disable-verity` command.

    Android Debug Bridge version 1.0.31
    
Eventually, after the device boots, replace the privileged app. Let's say it's called mtron.

    adb shell rm -rf /system/priv-app/mtron
    adb push mtron.apk /system/priv-app
    adb shell chmod 644 /system/priv-app/mtron.apk
    adb reboot
    
## Center justification in a TextView

    <TextView
        ...
        android:gravity="center"
        ...>
    </TextView>
    
  



    

    
