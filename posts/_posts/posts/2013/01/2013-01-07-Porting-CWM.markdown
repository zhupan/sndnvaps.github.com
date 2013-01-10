---
layout: post
uri: /posts/2013/01
permalink: /posts/2013/01/index.html
title: "Porting Clockwork Recovery to New Devices"
tags: [android,cwn,porting]
description: "Porting Clockwork Recovery to New Devices"
tagline: "Porting Clockwork Recovery to New Devices"
exerpt: |-

---

[origin link:](http://www.koushikdutta.com/2010/10/porting-clockwork-recovery-to-new.html)

Update/Preface:

It is difficult for me to port recovery for a device I don’t have. So, people can attempt to port it using this guide. However, if you want it done properly, and probably quicker, you can loan the device to me personally at:

Koushik Dutta 2721 1st Ave 507 Seattle, WA 98121

The package must include: 

 1. The rooted phone. 

 2. A return packing slip to your address.
 
 3. A signed statement saying: “I, <your name here>, am lending this device, <name of device>, to Koushik Dutta so that he can try to port Clockwork Recovery to the device. I understand that rooting a phone voids the warranty and tampering with the software may render the device nonfunctional. I realize and accept that the phone may not be functional when it is returned. Koushik Dutta is not liable for any damages to the device.” 
  4. BEFORE SENDING ME THE PACKAGE, CONFIRM WITH ME THAT I AM AVAILABLE TO PORT THE RECOVERY. 

It will take around a week, and there are no gaurantees whether I will actually be able to do it (due to proprietary software, locked bootloaders, my schedule, etc). After a week (generally quicker), I will send it back. I’m a trustworthy guy and am well known in the Android community. And I’ve already done this for several loaner devices. So you don’t need to worry about the safety of your precious hardware.

Otherwise, continue on the to the guide!

  1. This guide will assume you have some familiarity with doing an Android Build.
 
  2. This guide will work for phones that use a standard Android boot image format. This guide will not work for Samsung phones which use an initramfs. 

First, let's check out the CyanogenMod tree. The CyanogenMod repository contains Clockwork Recovery, which is part of a full Android build. 
{% highlight bash %}
repo init -u git://github.com/CyanogenMod/android.git -b gingerbread

repo sync

make -j4 otatools
 {% endhighlight %}
 

Now, use dump_image or dd to dump your recovery or boot image from a running phone and copy it to your computer somewhere. 

dump_image boot boot.img

To build Android from source for a new device, you need to set up a board config and its makefiles. This is generally a long and tedious process. Luckily, if you are only building recovery, it is a lot easier. From the root of your Android source directory (assuming you've run envsetup.sh), run the following (substituting names appropriately): 

{% highlight bash %}

build/tools/device/mkvendor.sh device_manufacturer_name device_name /your/path/to/the/boot.img
{% endhighlight %}



You will receive the confirmation "Done!" if everything worked. The mkvendor.sh script will also have created the following directory in your Android source tree: 

manufacturer_name/device_name 

Now, type the following: 

{% highlight bash %}
 lunch full_device_name-eng 
 {% endhighlight %}

This will set the build system up to build for your new device. Open up the directory in a file explorer or IDE. You should have the following files: AndroidBoard.mk, AndroidProducts.mk, BoardConfig.mk, device_.mk, kernel, system.prop, recovery.fstab, and vendorsetup.sh.

The two files you are interested in are recovery.fstab and kernel. The kernel in that directory is the stock one that was extracted from the boot.img that was provided earlier. For the most part, recovery.fstab will work on most devices that have mtd, emmc, or otherwise named partitions. But if not, recovery.fstab will need to be tweaked to support mounts and their mount points. For example, if your /sdcard mount is /dev/block/mmcblk1p1, you would need the following lines in your BoardConfig.mk: 
<pre>
  <code>

/sdcard vfat /dev/block/mmcblk1p1 
   </code>
</pre>

Once the recovery.fstab has been properly setup, you can build the recovery using:

{% highlight bash %}
 make -j4 recoveryimage 
{% endhighlight %}

Your recovery can then be found at $OUT/recovery.img. If you are in need of building a fakeflash recovery, you will need to run the following to create the update.zip that hot replaces the recovery: 
{% highlight bash %}
  make -j4 recoveryzip
{% endhighlight %}

Once this is done, build, and tested, notify me, "koush", on Github and I can build official releases and add ROM Manager support! 

Tip: Run "make clobber" between builds if you change the BoardConfig.mk, or the change will not get picked up.

**Github:**
 [https://github.com/koush](https://github.com/koush)

