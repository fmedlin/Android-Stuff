# Android-Stuff

## Replace a privileged system app for debug

With this version of adb (Mac):

    Android Debug Bridge version 1.0.35
    Revision 102d0d1e73de-android

Make /system writable by:

    adb root
    adb disable-verity
    adb remount
    adb reboot

Seems to take a few reboots sometimes before the remount succeeds.

It failed for me on an Ubuntu VM. It didn't understand the `disable-verity` command.

    Android Debug Bridge version 1.0.31
    
Eventually, after the device boots, replace the privileged app. Let's say it's called mtron.

    adb shell rm -rf /system/priv-app/mtron
    adb push mtron.apk /system/priv-app
    adb shell chmod 644 /system/priv-app/mtron.apk
    adb reboot
  
## Build Android N

When encountering this error on Mac: `Unsupported curl, please use a curl not based on SecureTransport ninja`

Replace curl with an SSL 

    brew install curl --with-openssl
    export PATH=$(brew --prefix curl)/bin:$PATH
    
H/T to [stack overflow](http://stackoverflow.com/a/35024131/42671)

## Center justification in a TextView

    <TextView
        ...
        android:gravity="center"
        ...>
    </TextView>
    
  



    

    
