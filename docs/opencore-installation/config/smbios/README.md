# SMBIOS

1. Prepare your config.plist which you've made.
2. Download or clone the whole repo of [GenSMBIOS](https://github.com/corpnewt/GenSMBIOS).
3. Open the folder and open GenSMBIOS.bat \(on Windows\) or right-click open GenSMBIOS.command \(on macOS\)
4. Enter 1 and enter. \(for update/install MacSerial\)
8. Enter 3 and enter.
9. Enter the SMBIOS you want to generate and enter the number of SMBIOS amount. Press enter. **For AMD System,** here is the list of SMBIOS recommended from the most to the least: 
    - _**iMacPro1,1**_ \(most recommended\) 
    - _**iMac14,2**_ \(also recommended\)
    * MacPro7,7 \(Exclusive for Catalina\)
    - MacPro6,1 \(a little bit old but it works\)
    - MacPro5,1 \(outdated and already lost support on Catalina\)
    - Other SMBIOS \(not recommended as they might cause problems\)
11. Go to [this website](https://checkcoverage.apple.com/) to check if your serial number is valid or not. We want a **valid** serial number BUT purchased date is not validated.
12. If you get an invalid serial number, finish. If not, redo the whole proccess until you have a **valid** serial number.
13. Copy all the SMBIOS information to a text file. We'll need that later.

Press [this](../../usb-opencore/) to continue configuring OpenCore in **windows** or [this](../../usb-opencore/#install-and-configuring-opencore-in-macos) to continue configuring OpenCore in **macOS**

<a href="#" onclick="window.history.back()">Go back</a>