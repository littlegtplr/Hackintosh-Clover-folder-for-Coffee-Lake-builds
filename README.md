# Kexts-and-plist
i5-8500 + B360 + ~~GTX 1060 6GB~~ RX580

Components used for this build: 

- Intel - Core i5-8500 3GHz 6-Core Processor
- Gigabyte - B360 AORUS Gaming 3 WIFI ATX LGA1151 Motherboard
- Corsair - Vengeance LPX 16GB (2 x 8GB) DDR4-3000 Memory 
- Crucial - MX500 500GB 2.5" Solid State Drive 
- ~~- EVGA - GeForce GTX 1060 6GB 6GB SSC GAMING Video Card~~ 
- Sapphire - Radeon RX 580 8 GB PULSE

### 16 May 2019 Update:
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



### 6 Jan 2019 Update:
- updated efi drivers and kexts to the latest
- removed '/Graphics/Inject Intel' and '/Graphics/ig-platform-if'
- updated '/Devices/Properties/PciRoot(0x0)/Pci(0x2,0x0)' and 'AAPL,ig-platform-id', 'framebuffer-patch-enable' and 'framebuffer-stolenmem' (see [vanilla guide](https://hackintosh.gitbook.io/-r-hackintosh-vanilla-desktop-guide/config.plist-per-hardware/coffee-lake#devices)), otherwise Mojave (10.14.2) would boot into a prohibit sign, -v shows 'unable to allocate runtime area'

### 14 Dec 2018 Update:
- updated efi drivers to the latest
- set SIP to disabled (CsrActiveConfig '0x67'), otherwise macOS 10.14.2 would boot into a prohibit sign, possibly due to not being able to load unsigned kexts (see [wiki](https://en.wikipedia.org/wiki/System_Integrity_Protection))

### 10 Dec 2018 Update:
- updated kext and efi drivers, also cleared some clutters

### 9 Nov 2018 Update:
- Jumped ship from nVidia to AMD. The plist can stay the same if you're just lazy or if it doesn't give you any issue. The only thing need to change when switching from nVidia to AMD is to tick *off* 'System Parameters/NvidiaWeb', but in my case it boots up without any issue with this option ticked, even with the web driver installed. 
- macOS updated to Mojave
- 'config.plist/Graphics/ig-platform-id' changed to '0x3E920003' (connectless UHD630) to get native support from Mojave
- remove igpu plist, currently not yet succeed to get iGPU works on Mojave. Use ig-platform-id '3E9B0007' can boot into Mojave but into black screens on either DVI or HDMI. This can possibly relate to framebuffer but I haven't managed to solve it. If you know how to do this, please share it with me. Cheers. 

### 26 Sep 2018 Update:
- Rename config_iGPU.plist to config.plist if you're using iGPU (for example the dGPU is in an RMA...)
- kexts and drivers were updated to latest
- The repo *should* be Majove ready, currently awaiting for nVidia's driver to test
- A custom USB SSDT was created in /ACPI/patched. It disables all unused USB ports on the mobo, plus the USB 3.0 capability of one of the front panel USB 3.0 ports. If you're not using the exact mobo, or you wish to use the port number patch instead, please don't include the 'ACPI' folder in your EFI, and enable the port limit patch, '10.13.6+ by PMHeart', in 'KernelAndKextPatches' in the plist.

For detailed description, please see my reddit post - https://www.reddit.com/r/hackintosh/comments/8px0ku/success_first_hackintosh_i58500b360gtx1060_6gb/

Or, my x230 repo has detailed steps on how to construct the whole thing - just need to be aware that the kexts and the plist are different. 
https://github.com/littlegtplr/Hackintosh-X230-macOS
