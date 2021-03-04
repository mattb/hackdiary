---
title: Installing Debian on a Dell Latitude X200
author: Matt Biddulph
type: post
date: 2003-03-09T20:54:36+00:00
excerpt: \n
url: /2003/03/09/installing-debian-on-a-dell-latitude-x200/
categories:
  - hardware
  - linux

---
_UPDATE: [more notes written recently][1]_

My new laptop arrived this week &#8211; a [Dell Latitude x200][2]. And it&#8217;s _marvellous_. Wonderfully lightweight, good battery life for such a small box, good keyboard and a really clear bright screen. After a quick look at Windows XP, which I&#8217;d never seen properly before, I set about installing Linux on it. The [Linux on Laptops Dell page][3] has links to some useful bootstrapping information, but there were a few things I found pretty hard to work out. Here are my notes on those things.

<!--more-->

  
**Re-partitioning the disk**  
The machine came with Windows XP installed on a single partition that covered the entire 30 gig disk. I didn&#8217;t want to delete it in case it comes in useful for something (games, perhaps), but I did want to scrunch it down to some sort of reasonable size. I used to have a copy of Partition Magic but it&#8217;s a pre-XP version and I couldn&#8217;t find it anyway. The obvious free alternative is [GNU Parted][4], but it runs under Linux. The laptop doesn&#8217;t come with a floppy drive, so bootdisks are no use. Even a bootable rescue CD isn&#8217;t that much use as I couldn&#8217;t find any distribution that had firewire drivers in its rescue kernel. The laptop&#8217;s BIOS can boot off the firewire DVD drive, but as soon as Linux takes control the drive effectively disappears and so the boot sequence can&#8217;t be completed.

The answer turns out to be [Knoppix][5], a fantastic piece of packaging work that gives you a complex Linux system (X, gnome, kde, mozilla, openoffice, etc) that runs entirely off a CD. It can&#8217;t run off a firewire CD either, but it turns out that if you copy the KNOPPIX directory from its CD onto the C: drive inside windows then boot off the CD, the initial ramdisk intelligently searches your hard disk and mounts from the KNOPPIX directory when it can&#8217;t find a CD. Parted is in Knoppix, and it was simple to resize the XP partition down to 5 gig following the documentation on the GNU site. Windows XP still boots fine, and I was able to go ahead with Linux install using a Debian CD copied to the C: drive.

**X Windows**  
The graphics chipset on the x200 is an Intel i830M. There is some support in XFree86 4.2 but it&#8217;s missing the XVideo and RENDER extensions, which are very useful for media playing and pretty fonts. Happily, the recently-released X version 4.3.0 has improved support. I&#8217;m currently using experimental debs while it makes its way into sid. The apt sources are:  
`deb https://www.penguinppc.org/~daniels/sid/$(ARCH) ./`  
`deb-src https://www.penguinppc.org/~daniels/sid/source ./`  
Here&#8217;s my [XF86Config-4][6]. There&#8217;s nothing unusual in there.

**Firewire DVD+CDRW drive**  
The drive (&#8220;Vendor: HL-DT-ST Model: RW/DVD GCC-4240N Rev: D110&#8221; according to syslog) works with kernel 2.4.20 using the ohci1394 and sbp2 modules. Reading and writing CDs gave no problems, but playing DVDs with mplayer or ogle shows a lot of jerkiness. I haven&#8217;t yet found a hack or firmware update that makes the DVD playback region-free.  
_Update:_ I tried playing DVDs again last night and saw good smooth playback. I think this might be due to the automatic power-based CPU speed adjustment. With the default BIOS settings, the laptop switches its speed down to 400Mhz to save power when on batteries. Playing a DVD with power plugged in (and so running at 933Mhz), ogle used around 50% CPU, which implies that 400Mhz wouldn&#8217;t be enough power. I assume that I was running on batteries when I wrote the above. Ogle also didn&#8217;t seem to mind playing Region 1 discs as long as I set the region in /etc/oglerc. All good news. For the moment I&#8217;ve changed the BIOS setting to never slow the CPU, even on batteries. It&#8217;d be nice to have control over the setting at runtime so I could make a choice based on my usage. [CPUFreq][7] seems to be the solution but the page says it isn&#8217;t being maintained any more.

**Brightness softkeys**  
The screen&#8217;s brightness can be adjusted using the Fn+Up and Fn+Down keys. Oddly, doing this freezes the machine with the stock Debian 2.4.20 kernel. The solution is to recompile the kernel with the option &#8220;Local APIC support on uniprocessors&#8221; (under &#8220;Processor type and features&#8221;) turned off, and the problem goes away.

**Modem**  
The modem works with the [PCTEL linux drivers][8] using the _i8xx_ hal option when compiling.

**Battery metering**  
Using 2.4.20, the APM battery metering seems a little incomplete. Gnome&#8217;s battery status applet reports &#8220;N/A&#8221; rather than showing a percentage battery remaining. The &#8220;apm&#8221; command shows a percentage but no estimated remaining time. I haven&#8217;t found any options that help.

 [1]: https://www.hackdiary.com/archives/000049.html
 [2]: https://www.euro.dell.com/countries/uk/enu/dhs/products/model_latit_latit_x200.htm
 [3]: https://www.linux-on-laptops.com/dell.html
 [4]: https://www.gnu.org/software/parted/
 [5]: https://www.knopper.net/knoppix/index-en.html
 [6]: https://www.hackdiary.com/misc/XF86Config-4.txt
 [7]: https://www.brodo.de/cpufreq/
 [8]: https://linmodems.technion.ac.il/pctel-linux/