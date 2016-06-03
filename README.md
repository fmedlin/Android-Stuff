# Android-Stuff

## Replace a privileged system app for debug

With this version of adb (Mac):

    Android Debug Bridge version 1.0.35
    Revision 102d0d1e73de-android

Make /system writable by:

    adb root
    adb disable-verity
    adb reboot
    adb remount

Seems to take a few reboots __sometimes__ before the remount succeeds.

It failed for me on an Ubuntu VM. It didn't understand the `disable-verity` command.

    Android Debug Bridge version 1.0.31
    
Eventually, after the device boots, replace the privileged app. Let's say it's called mtron.

    adb shell rm /system/priv-app/mtron/mtron.apk
    adb shell rm -rf /system/priv-app/mtron/oat  // if compiled with jack
    adb push mtron.apk /system/priv-app/mtron
    adb reboot
  
## Building Android from source

### Unsupported curl, please use a curl not based on SecureTransport ninja

When encountering this error on Mac, replace curl with an SSL 

    brew install curl --with-openssl
    export PATH=$(brew --prefix curl)/bin:$PATH
    
H/T to [stack overflow](http://stackoverflow.com/a/35024131/42671)

### Out of memory error

    GC overhead limit exceeded.
    Try increasing heap size with java option '-Xmx<size>'.
    Warning: This may have produced partial or corrupted output.
    
Try increasing the heap size. This worked for me:

    export ANDROID_JACK_VM_ARGS="-Xmx4g -Dfile.encoding=UTF-8 -XX:+TieredCompilation"

### What Android version am I building?

See the `BUILD_ID` value after executing the `lunch` command

    ...
    HOST_OS_EXTRA=Darwin-15.5.0-x86_64-i386-64bit
    HOST_CROSS_OS=
    HOST_CROSS_ARCH=
    HOST_CROSS_2ND_ARCH=
    HOST_BUILD_TYPE=release
    BUILD_ID=MOB30J
    OUT_DIR=out
    
Checkout the [source code tags](http://source.android.com/source/build-numbers.html#source-code-tags-and-builds) to lookup the `BUILD_ID` and find the branch and version that is being built.

## Center justification in a TextView

    <TextView
        ...
        android:gravity="center"
        ...>
    </TextView>
    
  



    

    
