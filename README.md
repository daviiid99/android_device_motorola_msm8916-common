# TWRP for Motorola MSM8916 Family
Heavily based on the Squid TWRP tree

## Dependencies:
(you probably don't need most of these)
```
sudo apt-get install bison build-essential curl flex git gnupg gperf libesd0-dev liblz4-tool libncurses5-dev libsdl1.2-dev libwxgtk2.8-dev libxml2 libxml2-utils lzop openjdk-6-jdk openjdk-6-jre pngcrush schedtool squashfs-tools xsltproc zip zlib1g-dev
sudo apt-get install g++-multilib gcc-multilib lib32ncurses5-dev lib32readline-gplv2-dev lib32z1-dev
```
You also need the repo tool for cloning Android source trees.

## Set up and get the repo:
```
mkdir ~/twrp-omni
cd ~/twrp-omni
repo init --depth=1 -u git://github.com/minimal-manifest-twrp/platform_manifest_twrp_omni.git -b twrp-9.0
mkdir -p .repo/local_manifests
```
Create a file .repo/local\_manifests/motorola.xml and paste this in
```
<?xml version="1.0" encoding="UTF-8"?>
<manifest>
    <project path="device/motorola/msm8916-common" name="chil360/android_device_motorola_msm8916-common" remote="github" revision="twrp-9.0" />
    <project path="device/motorola/osprey" name="chil360/android_device_motorola_osprey" remote="github" revision="twrp-9.0" />
    <project path="kernel/motorola/msm8916" name="chil360/android_kernel_motorola_msm8916" remote="github" revision="10.0" />
    <project path="vendor/qcom/opensource/cryptfs_hw" name="LineageOS/android_vendor_qcom_opensource_cryptfs_hw" remote="github" revision="lineage-15.1" />

    <remove-project name="android_bootable_recovery" />
    <project path="bootable/recovery" name="chil360/twrp_bootable_recovery" remote="github" revision="android-9.0" />
</manifest>
```

Now fetch the code
```
repo sync
```

## Building:
(first command may not be necessary)
```
export ALLOW_MISSING_DEPENDENCIES=true
source build/envsetup.sh
breakfast osprey
make clean
mka recoveryimage
```
