CM10 for the Droid Incredible

## Info
[**XDA Discussion thread**](http://forum.xda-developers.com/showthread.php?t=2607025)

### Initialize
[Setup Linux/OS X](http://source.android.com/source/initializing.html) - Please note: I use JDK6 but you can also use JDK7

### Prepare to download sources
```bash
mkdir ~/android/inc-cm-11.0
mkdir ~/bin
cd ~/android/cm10/
curl https://dl-ssl.google.com/dl/googlesource/git-repo/repo > ~/bin/repo
chmod a+x ~/bin/repo
repo init -u git://github.com/CyanogenMod/android.git -b cm-11.0
```

### Finish setting up repo
```bash
mkdir ~/android/cm-11.0/.repo/local_manifests
wget -O ~/android/inc-cm-11.0/.repo/local_manifests https://raw.github.com/zachf714/android_device_htc_inc/cm-11.0/Manifest/local_manifest.xml
```

### Download the source
```bash
cd ~/android/inc-cm-11.0
repo sync -j6
```
NOTE: This WILL take a long time.

### Build
Make sure we're in ~/android/inc-cm-11.0...
```bash
cd ~/android/inc-cm-11.0
```

### You may want to pick other cherry-picks out of the repopick script in device/htc/inc/Manifests
```bash

### List of cherry-picks/reverts used. the first two are required to build
```bash
cd build
git fetch https://gerrit.omnirom.org/android_build refs/changes/37/4537/2 && git cherry-pick FETCH_HEAD

cd external/iproute2
git revert 4c48963

cd frameworks/opt/telephony
git fetch http://review.evervolv.com/android_frameworks_opt_telephony refs/changes/58/9758/1 && git cherry-pick FETCH_HEAD
git fetch http://review.evervolv.com/android_frameworks_opt_telephony refs/changes/59/9759/1 && git cherry-pick FETCH_HEAD

```

Pull in the prebuilts, like (currently only self-added GooManager)...
```bash
./vendor/cm/get-prebuilts
```

And build!
```bash
. build/envsetup.sh && time brunch inc
```
