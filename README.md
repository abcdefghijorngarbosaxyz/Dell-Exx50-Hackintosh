# Dell Exx50 Hackintosh

[![OpenCore Version](https://img.shields.io/badge/OpenCore-0.8.0-green.svg)](https://github.com/SkyrilHD/Dell-Exx50-Hackintosh/)
[![GitHub release](https://img.shields.io/github/tag/SkyrilHD/Dell-Exx50-Hackintosh.svg)](https://github.com/SkyrilHD/Dell-Exx50-Hackintosh/releases/)
[![GitHub issues](https://img.shields.io/github/issues/SkyrilHD/Dell-Exx50-Hackintosh.svg)](https://github.com/SkyrilHD/Dell-Exx50-Hackintosh/issues/)

### This repo contains all the fixes for Exx50 on macOS Monterey.

### I need a [confirmation](https://github.com/SkyrilHD/Dell-Exx50-Hackintosh/discussions/2) if the EFI is working on other models, so I can complete my list. Thanks!

I noticed that my E7250 has nearly the same specs as other Exx50 models, so this repo was created. This will NOT replace the E7250 repo.

Tested on:

Model | Latitude E7250
------------- | ---------------
CPU | Intel Core i5-5300U
GPU | Intel HD Graphics 5500
RAM | 16GB DDR3 1600Mhz
Storage | SK hynix SC210 mSATA 128GB
WiFi | Intel Dual Band Wireless-AC 7265
GSM/LTE | Sierra Wireless AirPrime EM7305 (DW5809e)
Software | macOS 12.4 Monterey

## EFI Compatibility list

Exx50 model | Supported? | Additional notes
:----------: | :----------: | :----------:
13 7350 | _Yes_ | 2
3550 2015 | **Yes** | 3
E7450 | **Yes** | -/-
E7250 | **Yes** | -/-
E5550 | **Yes** | 1
E5450 | **Yes** | -/-
E5250 | _Yes_ | -/-
E3450 | _Yes_ | -/-

Bold: confirmed working

Italic: not confirmed

1: disable your dGPU (if you have one) with a SSDT

2: MacBook8,1 is not supported anymore, so use SMBIOS that comes with this EFI

3: Follow [this](https://github.com/SkyrilHD/Dell-Exx50-Hackintosh/issues/19#issuecomment-865314466) for full functionallity 

Disclaimer: The list was created based on the specs. Please correct my mistakes

## What works?

Everything...

## Download and Install

Go to the [Releases](https://github.com/SkyrilHD/Dell-Exx50-Hackintosh/releases/) page of this repo and download the latest release. Then, copy the EFI folder to your EFI partition... That's it.

## Graphical glitches in macOS

There are two ways to fix the horizontal glitches (as seen [here](https://github.com/newyb/Something-useful-of-E7250/blob/main/BUG2%20at%20sign.jpg)) in macOS.

1. (Recommended) Enable 'Enable Legacy Option ROMs' in the BIOS by clicking General>Advanced Boot Options. [Here](https://supportkb.dell.com/img/ka02R000000oLv9QAE/ka02R000000oLv9QAE_en_US_2.jpeg) is a picture of that option.

2. If you want to use pure UEFI as a workaround, you can use [one-key-hidpi](https://github.com/xzhih/one-key-hidpi). Download and run the code and select 'Enable HIDPI (with EDID)'. Then restart your computer and the glitches should be resolved.

## Intel WiFi

Starting with v2.3, AirportItlwm is included in the EFI but disabled to ensure stability. To enable Intel WiFi, enable it in the config. The EFI will only have stable versions of AirportItlwm. So if you want to experiment with Intel WiFi, you can do so by visiting the [itlwm repo](https://github.com/OpenIntelWireless/itlwm) and downloading the latest alpha build. Stability can be much worse, so use with caution! Also, do not forget to enable IntelBluetoothFirmware and BlueToolFixup in the config to enable Bluetooth on Monterey!

If you experience no internet with AirportItlwm, I suggest switching to itlwm and see if it works there.

Since Monterey, the Bluetooth implementation has changed and therefore causes issues such as: Bluetooth will be broken after sleep. As a workaround, typing the following command in Terminal may fix this issue: `sudo killall -9 bluetoothd BlueTool`

If you want Continuity features: Buy a Broadcom card on eBay or your trusted website. You can check the Dortania buyers guide to see which card is the better option: [Link](https://dortania.github.io/Wireless-Buyers-Guide/)

## Touchscreen

For touchscreen models, I also added VoodooI2C to take advantage of the touchscreen display. However, it is disabled. If you want to use it, you have to activate all VoodooI2C-related kexts in the config! Since v2.0 there is a new touchpad kext that also uses VoodooInput. So you need to disable VoodooInput that comes with VoodooPS2 and enable VoodooInput that comes with VoodooI2C, otherwise the system will not boot.

## USB

If you experience a USB port not working or you have issues with it, the result would be since this EFI uses a USBMap of E7250. You need to map your USB by following this [issue](https://github.com/SkyrilHD/Dell-Exx50-Hackintosh/issues/28). It would be very helpful to post a USBMap as pull request or on the issue page, so I can add it to the project.

## Recommended BIOS settings
<details>
  <summary>Expand BIOS settings</summary>
  
**General:**

* Boot sequence -> Boot List Option: UEFI
        
**System configuration:**
        
* Parallel Port: Disabled
* Serial Port: Disabled
* SATA Operation: AHCI
        
**Security:**

* TPM Security: Off
 
**Secure Boot:**

* Secure Boot: Disabled
  
**Power Management:**

* Wake on LAN/WLAN: Disabled
* USB Wake Support: Off

</details>

## How to Install macOS Monterey

There are two ways you can install Monterey:

1. If you have an already working macOS, download the Installer from the App Store and make a bootable Installer with `createinstallmedia` by using this command in Terminal: `sudo /Applications/Install\ macOS\ Monterey.app/Contents/Resources/createinstallmedia --volume /Volumes/MyVolume`

2. If you are using Windows, use [macrecovery.py](https://github.com/acidanthera/OpenCorePkg/tree/master/Utilities/macrecovery) from the offical [OpenCore release package](https://github.com/acidanthera/OpenCorePkg/releases/). Follow this [guide](https://dortania.github.io/OpenCore-Install-Guide/installer-guide/winblows-install.html) to understand how it works.

After you have created a bootable Installer, copy the EFI folder to the EFI partition and install as usual. After the installation, mount the EFI partition of the installed OS and copy the EFI folder to its partition.

## Screenshot

![About this Mac](https://user-images.githubusercontent.com/28839925/137376042-5502b29d-ef16-4ff2-8c92-8998c46662e1.png)


## Credits

Thanks to:

- me (for wasting my time writing this and providing fixes)
- acidanthera (for making an awesome bootloader)
- adyrosebrigg (for help and testing USB and dimmed screen on Windows)
- dortania (with their troubleshooting guide, I was able to fix sleep)
- DrHurt (for supporting our ALPS Trackpad)
- emrah7celik (for providing a guide on how to fix the glitches in macOS with pure UEFI)
- Harvé (for suggesting to inject property in Clover)
- hickorysb (for confirming the fix for glitches with Legacy Option ROMs)
- zxystd (for fixing the Bluetooth issue and Intel WiFi card)


All this was written on an E7250 with Monterey installed :D
