# Kexts-and-plist
i5-8500 + B360 + ~~GTX 1060 6GB~~ RX580

Components used for this build: 

- Intel - Core i5-8500 3GHz 6-Core Processor
- Gigabyte - B360 AORUS Gaming 3 WIFI ATX LGA1151 Motherboard
- Corsair - Vengeance LPX 32GB (4 x 8GB) DDR4-3000 Memory 
- Crucial - MX500 500GB 2.5" Solid State Drive 
- ~~- EVGA - GeForce GTX 1060 6GB 6GB SSC GAMING Video Card~~ 
- Sapphire - Radeon RX 580 8 GB PULSE

## To start, use the [OpenCore Vanilla Guide](https://dortania.github.io/OpenCore-Desktop-Guide/) and ask questions on [reddit/hackintosh](https://www.reddit.com/r/hackintosh/) if you encounter any issue. 

## 1 Jun 2020 Update:
- OC updated to 0.5.9
- macOS 10.15.5
- kexts updated

## 13 May 2020 Update:
- In BIOS/ there is a BIOS version offers CFG Lock option to lift up CFG Lock, from Gigabyte customer services. It should work but use at your own discretion. 

## 05 May 2020 Update:
- OpenCore updated to 0.5.8
- [Native CPU Power Management](https://dortania.github.io/OpenCore-Desktop-Guide/post-install/pm.html) enabled
  - Added OC/ACPI/SSDT-PLUG.aml, CPUFriend.kext and CPUFriendDataProvider.kext
  - Lifted [BIOS CFG Lock](https://dortania.github.io/OpenCore-Desktop-Guide/extras/msr-lock.html)
  - Disabled Kernel -> Quirks:
    - AppleCpuPmCfgLock
    - AppleXcpmCfgLock
    - If your BIOS is CFG Lock (pretty likely), these two quirks will need to be Enabled otherwise IT WON'T BOOT!
- Drivers and kexts updated to the latest
- Sanitary changes against the latest sample.plist and [OC tutorial](https://dortania.github.io/OpenCore-Desktop-Guide/config.plist/coffee-lake.html)
  - Removed EFI/OC/Drivers/ApfsDriverLoader.efi, as this is part of OC
  - Removed ACPI/Patch entries
  - Removed XHCI-300-series-injector.kext
- Vault set to Optional  

## 07 April 2020 Update:
- removed CPUFriend.kext and CPUFriendDataProvider.kext
- plist sanitary check against the latest OC manual/tutorial, various entries changed
- kext and drivers are updated to the latest
- macOS updated to 10.15.4

## 11 March 2020 Update:
- removed 'SMCBatteryManager.kext' and 'SMCLightSensor.kext' in 'Kernel/Add' and 'Kext'
- added NIC MAC address to 'PlatformInfo/Generic/ROM', you will need to put in your own as well. See [PlatformInfo](https://khronokernel-2.gitbook.io/opencore-vanilla-desktop-guide/intel-config.plist/coffee-lake#platforminfo)
- used [OC-Tool](https://github.com/rusty-bits/OC-tool/wiki) checked the plist and added/removed quite a few fields due to OC updates. 
- enabled Vault. Follow the procedure [here](https://khronokernel-2.gitbook.io/opencore-vanilla-desktop-guide/post-install/security#Vault) to sign your EFI off
- OpenCore updated to 0.5.6. 
- Just to summerise, to use my EFI for your machine, you will need to generate/fill in your own 'MLB', 'ROM', 'SystemSerialNumber' and 'SystemUUID' in 'PlatformInfo/Generic'. Then sign the EFI off using CreateVault that comes with OpenCore. 

## 4 February 2020 Update:
- kext updated to lastest
- OpenCore updated to 0.5.5
- macOS updated to 10.15.3

## 21 January 2020 Update:
- Added SSDT-PMC.aml to OC/ACPI/ for native NVRAM support. Also disabled plist: Booter/DisableVariableWrite and NVRAM/LegacyEnable. Then deleted nvram.plist in EFI. [Reference](https://www.reddit.com/r/hackintosh/comments/erd2th/nvram_for_all_300_series_users_rejoice/)

## 14 January 2020 Update:
- kext and drivers updated to the latest
- OpenCore updated to 0.5.4
- deleted 'UsbKbDxe.efi' due to my bluetooth keyboard doesn't need this
- deleted 'VirtualSmc.efi' as this has been implemented as part of OC 0.5.4 so no longer needed as an efi driver
- added EFI/OC/config.plist: MISC/Security/AllowSetDefault and set to 'TRUE'. This functionality enables assigning default booting partition from the booting picker, by either 'Ctrl + index' or 'Ctrl + Enter' if the chooser is used (use up and down arrow to activate it)
- EFI/OC/config.plist: MISC/Boot/Timeout set to '5' instead of '60', due to default booting partition is working properly
- Optional: if not doing multi-booting, then MISC/Boot/ShowPicker can be set to 'FALSE' to skip the picker

## 11 December 2019 Update:
- macOS updated to 10.15.2
- OpenCore updated to 0.5.3 December 2019 build
- kext and driver updated to lastest

## 30 October 2019 Update:
- macOS updated to 10.15.1
- OpenCore updated to 0.5.2
- kexts and drivers updated to the latest

## 10 October 2019 Update:
### Bootloader changed from Clover to OpenCore 0.51
- BIOS DVMT changed from 64MB to 32MB, otherwise OpenCore won't boot
- FakeSMC has been replaced by VirtualSMC, not necessary but was advised by [opencore-vanilla-desktop-guide](https://khronokernel-2.gitbook.io/opencore-vanilla-desktop-guide/)
- EFI/OC/config.plist: Platforminfo/Generic/System UUID, MLB and SystemSerialNumber are removed. You will need to generate your own system info by following the [platforminfo guide](https://khronokernel-2.gitbook.io/opencore-vanilla-desktop-guide/config.plist/coffee-lake#platforminfo) and enable NVRAM emulation with [NVRAM Emulated](https://khronokernel-2.gitbook.io/opencore-vanilla-desktop-guide/post-install/nvram). Use Xcode to edit the plist. 
#### Two functionality differences between Clover and OpenCore in my case:
- How the boot menu operates: I constantly dual boot between windows (for gaming) and macOS (for everything else). Currently, without a further update from the OpenCore team, each time will need to choose which partition to boot while booting up, hence the timeout has been set to 60 seconds. Otherwise the default booting option is the first partition, and often it is an EFI, which probably won't fit the flow in most cases. 
  - Such restriction is due to assigning default booting option with OpenCore is working with mobos with native compatible NVRAM (likely to be Z370). For any other mobos, the NVRAM is emulated with OpenCore (and it works nicely). However, with emulated NVRAM, the assignment via Startup Disk Preference Panel takes no effects at all. See [my post](https://www.insanelymac.com/forum/topic/338516-opencore-discussion/?do=findComment&comment=2692886) and [this reply](https://www.insanelymac.com/forum/topic/338516-opencore-discussion/?do=findComment&comment=2692986) for details. 
  - Workaround: only if you don't need dual booting - in config.plist, set Misc/Security/ScanPolicy to '0x10103' if your macOS is on a SATA device, or '0x80103' if your macOS is on a NVMe device (more details in [OpenCore manual/8.5.6 ScanPolicy](https://github.com/acidanthera/OpenCorePkg/blob/master/Docs/Configuration.pdf)). Either way should be able to make your macOS to be on the first entry while booting up. Once verify the booting is working as expected, in config.plist, Misc/Boot/ShowPicker can be set to 'False'. In this case OpenCore will straightly boot into the default partition, without prompting the boot picker and can minimise booting time. 
- NVRAM emulation: as mentioned above, the NVRAM emulation works quite well in my case. It solved the issue of shutting down/rebooting kernel panic with Clover, and now my hackintosh has been able to sleep with Catalina (though with Mojave bluetooth went missing once awake...another story). So it's a big plus to me, though the booting menu isn't ideal. YMMV. 
### macOS updated to 10.15 Catalina
- drivers and kexts are updated to the latest
- An EC device SSDT (SSDT-EC-USBX.aml) was added to EFI/OC/ACPI. Whether you need this, just use [USBMap](https://github.com/corpnewt/USBMap) to check whether your USB power setting is in place. If so then no further action is needed. 
- The macOS update was done by using System Preferences, rebooted once into the installer, then the next reboot is to Catalina. No issues encountered. 

## 29 July 2019 Update:
- macOS updated to 10.14.6
- kexts updated to latest
- Clover Bootloader updated to r5018, driver folder structure changed 
  - removed OsxFatBinaryDrv-64.efi
  - can't boot with OsxAptioFix3Drv.efi - couldn't allocate runtime area, use AptioMemoryFix-64.efi instead

## 16 May 2019 Update:
- macOS updated to 10.14.5
- updated efi drivers and kexts to the latest
- SMBIOS changed from iMac18,3 to iMac19,1 for better power management (PM), idle frequency increased to 1.3GHz from 0.8GHz (see below)

- added CPUFriend.kext and CPUFriendDataProvider to decrease the idle frequency back to 0.8GHz, by changing the four values in the frequency vector of iMac19,1 (Mac-AA95B1DDAB278B95.plist) from 0D to 08. Credit goes to [TheRacerMaster
](https://www.reddit.com/r/hackintosh/comments/9uh1wz/laptop_idles_at_a_higher_frequency_as_compared_to/) and [acidanthera/CPUFriend](https://github.com/acidanthera/CPUFriend)
   
   |iMac18,3 | iMac19,1 |iMac19,1 w/ CPUFriend|
   |:--------:|:------:|:------:|
   |<img width="200" src="https://github.com/littlegtplr/Hackintosh-Clover-folder-for-Coffee-Lake-builds/blob/master/img/Screenshot%202019-05-15%20at%2020.08.17.png">| <img width="200" src="https://github.com/littlegtplr/Hackintosh-Clover-folder-for-Coffee-Lake-builds/blob/master/img/Screenshot%202019-05-15%20at%2018.12.22.png">| <img width="200" src="https://github.com/littlegtplr/Hackintosh-Clover-folder-for-Coffee-Lake-builds/blob/master/img/Screenshot%202019-05-16%20at%2000.50.44.png"> |
   
- 'AAPL,ig-platform-id' changed from '0300923E' to '0300983E'. Either '0300913E' or '0300923E' will break the CPU PM - idle frequency will never get down to lower than 2GHz. Don't know why. '0300913E' is automatically assigned by macOS/WhateverGreen (but it breaks CPU PM) if no properties was assigned by the plist.
- changing SMBIOS and adding CPUFriend has negligible effects on performance
  
  Geekbench scores
  
   |  |Single Core| Multi Core|
   |:---|:-----------:|:-----------:|
   |[iMac18,3](https://browser.geekbench.com/v4/cpu/13145840) |5454 | 22299|
   |[iMac19,1](https://browser.geekbench.com/v4/cpu/13145531) |5432 | 22228|
   |[iMac19,1 w/ CPUFriend](https://browser.geekbench.com/v4/cpu/13148422) |5515 | 22000|



## 6 Jan 2019 Update:
- updated efi drivers and kexts to the latest
- removed '/Graphics/Inject Intel' and '/Graphics/ig-platform-if'
- updated '/Devices/Properties/PciRoot(0x0)/Pci(0x2,0x0)' and 'AAPL,ig-platform-id', 'framebuffer-patch-enable' and 'framebuffer-stolenmem' (see [vanilla guide](https://hackintosh.gitbook.io/-r-hackintosh-vanilla-desktop-guide/config.plist-per-hardware/coffee-lake#devices)), otherwise Mojave (10.14.2) would boot into a prohibit sign, -v shows 'unable to allocate runtime area'

## 14 Dec 2018 Update:
- updated efi drivers to the latest
- set SIP to disabled (CsrActiveConfig '0x67'), otherwise macOS 10.14.2 would boot into a prohibit sign, possibly due to not being able to load unsigned kexts (see [wiki](https://en.wikipedia.org/wiki/System_Integrity_Protection))

## 10 Dec 2018 Update:
- updated kext and efi drivers, also cleared some clutters

## 9 Nov 2018 Update:
- Jumped ship from nVidia to AMD. The plist can stay the same if you're just lazy or if it doesn't give you any issue. The only thing need to change when switching from nVidia to AMD is to tick *off* 'System Parameters/NvidiaWeb', but in my case it boots up without any issue with this option ticked, even with the web driver installed. 
- macOS updated to Mojave
- 'config.plist/Graphics/ig-platform-id' changed to '0x3E920003' (connectless UHD630) to get native support from Mojave
- remove igpu plist, currently not yet succeed to get iGPU works on Mojave. Use ig-platform-id '3E9B0007' can boot into Mojave but into black screens on either DVI or HDMI. This can possibly relate to framebuffer but I haven't managed to solve it. If you know how to do this, please share it with me. Cheers. 

## 26 Sep 2018 Update:
- Rename config_iGPU.plist to config.plist if you're using iGPU (for example the dGPU is in an RMA...)
- kexts and drivers were updated to latest
- The repo *should* be Majove ready, currently awaiting for nVidia's driver to test
- A custom USB SSDT was created in /ACPI/patched. It disables all unused USB ports on the mobo, plus the USB 3.0 capability of one of the front panel USB 3.0 ports. If you're not using the exact mobo, or you wish to use the port number patch instead, please don't include the 'ACPI' folder in your EFI, and enable the port limit patch, '10.13.6+ by PMHeart', in 'KernelAndKextPatches' in the plist.

For detailed description, please see my reddit post - https://www.reddit.com/r/hackintosh/comments/8px0ku/success_first_hackintosh_i58500b360gtx1060_6gb/

Or, my x230 repo has detailed steps on how to construct the whole thing - just need to be aware that the kexts and the plist are different. 
https://github.com/littlegtplr/Hackintosh-X230-macOS
