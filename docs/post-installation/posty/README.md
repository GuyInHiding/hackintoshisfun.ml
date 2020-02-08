# Posty!!!

## General

Download link for [Clover Configurator](https://mackie100projects.altervista.org/download-clover-configurator/)

?> If the newest link doesn't work, download an older one instead.

## Mount EFI

You'll always need to mount EFI for modification.

1. Open Terminal.
2. Run `diskutil list`
3. Find the Identifier of the EFI partition in your macOS disk.
4. Run `sudo diskutil mount <the identifier of the EFI>`
5. Enter your password.
6. Done.

## Clover Installation

We'll need to install Clover to your hard disk. Without that, you won't be able to boot to macOS.

1. Download Clover Install Package.
2. Right-click and press Open.
3. Keep pressing `Continue` until you get to Installation Type.
4. Press `Change Install Location..`.
5. Choose the hard disk you have your macOS installed and press `Continue`.
6. Press `Customize` and Choose these settings:
    ```
    Clover for UEFI booting only
    Install Clover in the ESP
    Recommended Drivers:  
    - ApfsDriverLoader
    - AptioMemoryFix
    - HFSPlus
    Install RC Scripts on target volume (or Install RC Scripts on other volumes)
    ```
7. Press Install.
8. When it finish, a partition call EFI should be mounted.
9. Mount your USB EFI partition.
10. Copy the kexts and config to your EFI partition \(like what you do before\)
11. Done.

## Audio

### AppleALC \(on Ryzen ONLY\)

#### Recommended way (Device Properties)

1. Mount the EFI partition of your disk
2. Download AppleALC.kext and put it to `EFI/CLOVER/kexts/Other` if you haven't yet
3. Download the latest release of [gfxutil](https://github.com/acidanthera/gfxutil/releases)
4. Open Terminal
5. Drag and drop the downloaded gfxutil to the Terminal Window and type `-f HDEF`
6. **If you do not have output, read** [how to change AZAL to HDEF](/post-installation/posty.md#change-azal-to-hdef) **first and run again**
7. The output should be something like this: `PciRoot(0x0)/Pci(0x1f,0x3)`
8. Go to the Specification page of your Motherboard on the official site and find the Audio Codec on your board
9. Go to [this page](https://github.com/acidanthera/AppleALC/wiki/Supported-codecs) and find your layout of your Codec. A layout should be a _**NUMBER.**_ A Codec should have more than one Layout ID. But if it isn't listed out, unfortunately you need to use VoodooHDA.
10. Open config.plist in the EFI partition with Clover Configurator or ProperTree Plist Editor
11. Go to Devices &gt; Properties and add the properties below
12. Save and reboot.


**Example:**

| Devices | Properties Key | Properties Value | Value Type |
| :--- | :--- | :--- | :--- |
| PciRoot\(0x0\)/Pci\(0x1f,0x3\) | layout-id | 07 | DATA |

?> If the above method doesn't work, try the [alternative method](#alternative-way-boot-arg)

#### Alternative Way (Boot arg)

1. Mount the EFI partition of your disk
2. Download AppleALC.kext and put it to `EFI/CLOVER/kexts/Other` if you haven't yet
3. Go to [this page](https://github.com/acidanthera/AppleALC/wiki/Supported-codecs) and find your layout of your Codec. A layout should be a _**NUMBER.**_ A Codec should have more than one Layout ID. But if it isn't listed out, unfortunately you need to use VoodooHDA
4. Open config.plist in the EFI partition with Clover Configurator or ProperTree Plist Editor
5. Go to Boot &gt; Boot Args and add `alcid=XX` (eg: alcid=1)
6. Save and reboot

!> Note: You'll loss 3.5mm Audio Input \(Microphone\) support. But VoodooHDA will fix it. NO FX SUPPORT

### VoodooHDA

* Nothing to do. Audio should work OOB.

!> Note: Worse audio quality than AppleALC.

### Change AZAL to HDEF

1. Mount the EFI partition.
2. Open config.plist with Clover Configurator or ProperTree Plist Editor.
3. Add the patch below in ACPI &gt; Patches section.
4. Save and reboot.

| Comments | Find | Replace | TgtBridge | Disabled |
| :--- | :--- | :--- | :--- | :--- |
| change AZAL to HDEF | 415A414C | 48444546 | &lt;empty&gt; | FALSE |

