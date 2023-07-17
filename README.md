# Dell Precision 5550 with macOS Ventura

A collection of all files needed to run Ventura on a Dell Precision 5550.

## Overview

This is more of a compilation of information and configs from various repositories and forums than a place where real development happens. This repository should contain everything needed to get Ventura up and running on your Dell Precision 5550 laptop.

## Status

| Hardware                      | Model                                    | Status        | Comments                                                     |
| ----------------------------- | ---------------------------------------- | ------------- | ------------------------------------------------------------ |
| **CPU**                       | Intel Core i7-10875H                     | ✅ Working     |                                                              |
| **eGPU**                      | NVIDIA Quadro T2000 Max-Q - 4 GB VRAM    | ❌ Not working | Will never work because of relations between NVIDIA and Apple.  |
| **iGPU**                      | Intel UHD Graphics 630                   | ✅
Working     |                                                              |
| **Internal Display**          | 1920x1200@60Hz                           | ✅ Working     | Internal display fully working including Backlight control. |
| **External Display(s)**       |                                          | ✅ Working     | Tested on a monitor with following specs - 3840x2160@60Hz . |
| **SSD**                       | Samsung EVO 970 Plus 250GB               | ✅ Working     |                                                              |
| **Trackpad**                  |                                          | ✅ Working     | Working with full gesture support (5 fingers).               |
| **Wi-Fi/ BT**                 | Intel Wi-Fi 6 AX201 160MHz               | ❌ Not working | The stock Intel AX Wi-Fi 6 card needs to be swapped out to a compatible card. |
| **LAN**                       | Intel I219-LM                            | ✅ Working     |                                                              |
| **Thunderbolt/ USB-C**        |                                          | ✅ Working     | USB-C charging works. Thunderbolt and USB-C devices are working. |
| **USB**                       |                                          | ✅ Working     | All Ports fully working with USB 2.0, 3.0 and 3.1/3.2 speed  |
| **Internal Speakers**         | Realtek ALC3204                          | ✅ Working     |                                                              |
| **Internal Microphone array** |                                          | ✅ Working     |                                                              |
| **Headphone Jack**            |                                          | ✅ Working     | Works, including automatic switch to headphone if plugged in. |
| **Webcam**                    |                                          | ✅ Working     |                                                              |
| **SDXC reader**               | Realtek RTS452A                          | ✅ Working     |                                                              |
| **Fingerprint reader**        |                                          | ❌ Not working | Will never work, because of MacBooks with TouchID and T2 chip and proprietary Windows drivers for Dell. |

| Features                   | Status         | Comments                                                     |
| -------------------------- | -------------- | ------------------------------------------------------------ |
| **Sleep**                  | ❌ Not working |                                                              |
| **Lid Open/Close**         | ❌ Not
working |                                                              |
| **iMessage and App Store** | ✅ Working     | Need tinkering.          |
| **Handoff**                | ✅ Working     | Tested with iPhone 13 Pro             |
| **Sidecar**                | ✅ Working     | Tested with iPad Pro M2                                   |
| **Watch Unlock**           | ✅ Working     | Tested with Apple Watch series 5        |
| **FileVault 2**            | 🔶 Partially   | Encryption itself is working fine but generates a small boot delay (20 seconds) until asking for the FileVault password.

## Installation

### BIOS/UEFI settings

- Secure Boot: Off (Default: On)
- SATA Mode: AHCI (Default: RAID)
- Intel SGX: Software Controlled or Off

### Wi-Fi/Bluetooth

The stock Intel Wi-Fi cards are still unstable in macOS. So to use Wi-Fi with "AirPort feeling", you will have to replace it for a supported card. However this is harder said then done. The installed Intel card is soldered to the motherboard. It is possible to buy a connector and use the second ssd slot to instal the other card. However afterwards the new card and the existing antenas have to be fitted with new prolonged cables, which are hard to get by. The other possibility is to try to use the following kext [itlwm](https://github.com/OpenIntelWireless/itlwm). Its an interesting and promissing project, which tries reverse engineer the drivers for the card.

### Performance

CPU power management is done by `CPUFriend.kext` while `CPUFriendDataProvider.kext` defines how it should be done. `CPUFriendDataProvider.kext` is generated for a specific CPU and power setting. The one supplied in this repository was made for the Intel Core i7-10875H and is optimized for optimized performance.

## Kexts
The following kexts are present:
- Airportitlwm.kext: Intel wifi, sometimes works, mostly not.
- AppleALC.kext: Support for audio.
- AppleRTL815XEthernet110.kext: Support for ethernet.
- BlueToolFixup: Bluetooth for macos.
- BrigtnessKeys: Allow using FN keys to adjust brightness, is not bound to the default keys.
- CPUFriend: Change the performance model of the CPU.
- CPUFriendDataProvider: Specification of the performance model.
- IntelBluetoothFirmware: Bluetooth for intel cards.
- Lilu: required - dependency to lot of other kexts.
- NoTouchID: no touchid popups will appear - nothing appeared during testing.
- NVMeFix: ssd support - non apple NVMe.
- SMCBatteryManager: monitoring, especially battery.
- SMCDellSensors: monitoring, especially fans on dell.
- SMCLightSensor: monitoring, especially ambient light sensor.
- SMCProcessor: monitoring, especially cpu temperature.
- SMCSuperIO: monitoring, especially fans.
- USBInjectAll: USB.
- UsbPorts: mapping of the ports on the machine.
- VirtualSMC: required - emulates SMC chip on macs
- VoodooI2C: required - keyboard, mice, trackpad
- VoodooI2CHID: required - keyboard, mice, trackpad
- VoodooPS2Controller: required - keyboard, mice, trackpad
- WhatteverGreen: required - enables graphics

While I have chosen these texts, I want to clarify that I'm not claiming it to be the optimal choice. I acknowledge that there are areas that could be enhanced.

## Conclusion
Because of the sleep issues and the lack of a proper Wi-Fi card, I decided to use this project solely for experimenting with macOS, specifically Hackintoshing. It was a fantastic experience, and I gained a lot of knowledge about low-level stuff, particularly the interaction between actual computer components and the operating system. If you enjoy tinkering with fascinating things, I can highly recommend this hobby project. Feel free to add improvements via PR and report issues 🙂.

Happy hacking!

## Credits

- [Apple](http://apple.com/) for providing macOS

- [dortania](https://dortania.github.io/OpenCore-Install-Guide/) for providing OpenCore and documentation

- [acidanthera](https://github.com/acidanthera) for providing almost all kexts and drivers

- [vit9696](https://github.com/vit9696) for providing Lilu.kext

- [alexandred](https://github.com/alexandred) for providing VoodooI2C

- [RehabMan](https://github.com/RehabMan) for providing many laptop [hotpatches](https://github.com/RehabMan/OS-X-Clover-Laptop-Config/tree/master/hotpatch) and guides

- [jaromeyer](https://github.com/jaromeyer/XPS9570-Catalina) for providing the readme template with tutorials and status tables.

- [al3xtjames](https://github.com/al3xtjames) for providing the  plugin for disabling Touch ID support.

- [MokkaSchnalle](https://github.com/MokkaSchnalle) Providing his configuration file inspired me for this creation, and our configuration is very similar.
