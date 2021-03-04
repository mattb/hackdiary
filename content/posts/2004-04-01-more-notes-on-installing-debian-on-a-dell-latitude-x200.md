---
title: More notes on installing Debian on a Dell Latitude X200
author: Matt Biddulph
type: post
date: 2004-04-01T23:06:01+00:00
excerpt: \n
url: /2004/04/01/more-notes-on-installing-debian-on-a-dell-latitude-x200/
categories:
  - hardware

---
[Last year I bought a Dell Latitude X200 laptop][1], which was a wonderful machine. In October it was stolen from my flat in a break-in. I made do with a refurbished [HP Omnibook 500][2] but I wasn&#8217;t happy with it. When a 2nd-hand X200 came up on ebay last week at a good price, I couldn&#8217;t resist snapping it up. In the time since I last installed linux on one of these machines, there have been a few developments and new releases that make installation and configuration easier.

<!--more-->

  
Last time round, I had to install by resizing the installed Windows XP partition via a complicated process using Knoppix booted from the C: drive This was because none of the Debian boot disks had the requisite Firewire support to see the CDROM after the BIOS handed over control during the boot sequence. This time round, I discovered that there are now newer [boot ISO images][3] available which include Firewire. Using the Windows cd recording software, I burnt the bf2.4 image and booted from it. Once in Linux, I just needed to remove and reload the sbp2 module to get it to recognise the drive as /dev/sda (for some reason it didn&#8217;t work when the module is first autoloaded). I then finished the install over the net, first using the 3c59x driver to get wired ethernet, then (once it was bootstrapped up to a level where wireless-tools would run) the orinoco_cs driver for the internal TrueMobile 1150 wireless.

The 2.6 kernel series has moved on since I last tried it, and I found 2.6.4 works very well. Here&#8217;s the [.config][4] I&#8217;m currently using.

Lincoln Stein has been doing great work [documenting his struggles][5] with the X200, and provides a very useful howto and patch to [modify the ACPI DSDT][6] to allow ACPI to read your battery levels under Linux. If you&#8217;re going to do this, I highly recommend [patching your kernel][7] to allow DSDTs to be loaded on the fly at boot rather than compiling them in.

ACPI S3 suspend still locks my machine dead (to the extent that it doesn&#8217;t even listen to the power button and the battery needs to be removed and replaced before it&#8217;ll turn on again). I&#8217;d love to get suspend working if anyone knows how. [Edd][8] tells me that he has exactly the same problem with his Sony TR1MP, which also uses an Intel i8xx chipset.

I&#8217;ve had a brief go at getting [Software Suspend][9] working, and had middling success. The combination of 2.6 kernel, swsusp and AGP is known to not work on several systems, and the X200 is one of them. However, if I prevent X and hotplug from loading the i830, intel_agp and agpgart modules (thus losing XVideo support in X), it works. I need to do a bit of finetuning of module reloading and device reconfiguration on resume, but it looks promising.

With the 2.6 kernel, the performance and powersaving modes of the Pentium 3M CPU can now be controlled from linux. I installed the _cpudyn_ daemon and now my system switches automatically into performance mode when CPU usage goes over 50%, and stays in powersaving mode otherwise.

As of March 2004, there&#8217;s a very neat driver for the touchpad available in Debian sid. The package is called _xfree86-driver-synaptics_ and lets you use the touchpad as more than just an emulated PS/2 mouse. The driver enables basic features such as acceleration and tap control, and adds some very neat stuff like the ability to scroll the current window by moving up and down on the far right of the touchpad (comparable to mousewheel scroll on a wheelmouse).

My first X200 came with a nice external firewire DVD/CDRW drive, which could be hotplugged with no problems. The new one came with the docking station, which has the same drive in it, but now it only appears on the firewire bus if I boot the laptop in the docking station. If I boot without it then later dock the laptop, the drive doesn&#8217;t appear even if I unload and reload the Firewire kernel modules.

 [1]: https://www.hackdiary.com/archives/000025.html
 [2]: https://www.obviously.com/laptops/OmniBook500linux
 [3]: https://people.debian.org/~blade/boot-floppies/cvs/
 [4]: https://www.hackdiary.com/misc/dotconfig-x200-2.6.4.txt
 [5]: https://modperl.com:9000/x200/
 [6]: https://modperl.com:9000/x200/dsdt_details.html
 [7]: https://gaugusch.at/kernel.shtml
 [8]: https://usefulinc.com/edd
 [9]: https://swsusp.sourceforge.net/