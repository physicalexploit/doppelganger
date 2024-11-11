# Doppelgänger Community Edition

![Doppelgänger Logo](https://github.com/optiv/doppelganger/blob/main/git_images/dop_logo.png)

Doppelgänger is firmware that runs on ESP32 devices that can be embedded within commercially available RFID readers with the intent of capturing access control card data while performing physical security assessments. Doppelgänger keeps the operator's ease of access, maintenance, and operational communications in mind.

## Supported Card Types

Doppelgänger Community Edition officially supports the processing of Wiegand data for the following card types:

* HID H10301 26-bit
* Indala 26-bit (requires Indala reader/module)
* Indala 27-bit (requires Indala reader/module)
* Indala 29-bit (requires Indala reader/module)
* HID D10202 33-bit
* HID H10306 34-bit
* HID Corporate 1000 35-bit
* HID H10304 37-bit

For expanded card support and keypad applications, consider purchasing Doppelgänger Pro, Stealth, or MFAS (Multi-Factor Stealth) from the [Physical Exploitation Store](https://store.physicalexploit.com/). Below are the officially supported card types for premium devices:

| Card Types                  | Community Edition | Pro | Stealth | MFAS | Notes                         |
| --------------------------- | ----------------- | --- | ------- | ---- | ----------------------------- |
| Keypad PIN Codes            |                   |     |         | X    |                               |
| HID H10301 26-bit           | X                 | X   | X       | X    |                               |
| Indala 26-bit               | X                 | X   | X       | X    | Requires Indala reader/module |
| Indala 27-bit               | X                 | X   | X       | X    | Requires Indala reader/module |
| 2804 WIEGAND 28-bit         |                   | X   | X       | X    |                               |
| Indala 29-bit               | X                 | X   | X       | X    | Requires Indala reader/module |
| ATS Wiegand 30-bit          |                   | X   | X       | X    |                               |
| HID ADT 31-Bit              |                   | X   | X       | X    |                               |
| EM4102 / Wiegand 32-bit     |                   |     | X       | X    |                               |
| HID D10202 33-bit           | X                 | X   | X       | X    |                               |
| HID H10306 34-bit           | X                 | X   | X       | X    |                               |
| HID Corporate 1000 35-bit   | X                 | X   | X       | X    |                               |
| HID Simplex 36-bit (S12906) |                   | X   | X       | X    |                               |
| HID H10304 37-bit           | X                 | X   | X       | X    |                               |
| HID Corporate 1000 48-bit   |                   | X   | X       | X    |                               |
| C910 PIVKey                 |                   |     | X       | X    |                               |
| MIFARE (Various Types)      |                   |     | X       | X    |                               |

## Background

This project stemmed from the Raspberry Pi chip shortage, which drove up the cost of RPi Nano W boards making the cost to repair the team's long-range cloners not feasible. In addition, there were some limitations with existing tooling that I aimed to mitigate.

## Intent

This project intended to accomplish the following:

1) Use modern/actively supported CoTS equipment that can easily be replaced.
2) The operator can't go into a comms blackhole while connected to the device.
3) Egress for notifications, reducing the need to check for card reads while in the middle of an operation.
4) Simplified WebGUI that only displays Bit Length, Facility Code, and Card Number. Option to download the complete data set(e.g., BL, FC, CC, HEX, BIN).
5) Error handling, so the device doesn't display bad reads or EMI in the main card log.
6) Easy configuration and reset functionality for team use.

## Integration Options

The simpliest way to get going with Doppelgänger is to head over to the [Practical Physical Exploitation Store](https://store.physicalexploit.com/) and purchase a pre-built longrange reader, stealth, MFAS, or Breakout board. To view the support documents for premium hardware, you can reference the [Practical Physical Exploitation Documentation](https://physicalexploit.com/docs/products/getting-started/).

### Longrange Readers

* [HID MaxiProx 5375 Longrange Wiegand Data Interpreter](https://store.physicalexploit.com/products/hid-maxiprox-5375-longrange-wiegand-data-interpreter): Supports HID Prox card types. Inculdes Doppelgänger Pro Firmware.
* [HID iCLASS R90SE Longrange Wiegand Data Interpreter](https://store.physicalexploit.com/products/hid-iclass-r90se-longrange-weigand-data-interpreter): Supports iCLASS Legacy/SE/Seos card types. Inculdes Doppelgänger Pro Firmware.

### Non-Destructive Skimmers

* [Doppelgänger Breakout Board (Fully Assembled)](https://store.physicalexploit.com/products/doppelganger-pcb?variant=47805447045433): Comes with Doppelgänger Community Edition firmware pre-installed.
* [Doppelgänger Breakout Board (DIY Kit)](https://store.physicalexploit.com/products/doppelganger-pcb?variant=47805447045433): User will need to provide their own SparkFun Thing Plus C board.

* [Stealth Wiegand Data Interpreter](https://store.physicalexploit.com/products/ghost-reader?variant=48388730749241): Supports Prox, EM, AWID, PIV, MIFARE, iCLASS Legacy/SE/Seos. Indala is supported on certain models but removes Prox, EM, and AWID. This is a hardware limitation by HID not a Doppelgänger limitation. Runs on Doppelgänger Stealth firmware.
* COMING SOON Multi-Factor Stealth (MFAS) Wiegand Data Interpreter: Supports PIN Codes, Prox, EM, AWID, PIV, MIFARE, iCLASS Legacy/SE/Seos. Indala is supported on certain models but removes Prox, EM, and AWID. This is a hardware limitation by HID not a Doppelgänger limitation. Runs on Doppelgänger MFAS firmware.

### Doppelgänger Breakout Board

* [Doppelgänger Longrange Breakout Board](https://store.physicalexploit.com/products/doppelganger-pcb): Supports HID MaxiProx 5375 and HID iCLASS R90SE

![Doppelgänger Longrange Breakout Board](https://github.com/optiv/doppelganger/blob/main/git_images/doppelganger_pcb.jpg)

![Doppelgänger MaxiProx 5375](https://github.com/optiv/doppelganger/blob/main/git_images/maxiprox.jpg)

## DIY Build

The Doppelgänger firmware is designed to work with the [SparkFun Thing Plus - ESP32 WROOM (USB-C)](https://www.sparkfun.com/products/20168), which employs the Espressif ESP32-WROOM-32E chip. *Note, other ESP32 boards may be used but modifications to the firmware will be required.*

### Wiring Doppelgänger to a RFID Reader

Only attempt to build this device if you know what you're doing. The developer is not responsible for damaged equipment/property. Doppelgänger has been tested on the following devices, but it should work on any reader that outputs a Weigand signal:

* HID MaxiProx 5375AGN00
* HID ICLASS SE R90 940NTNTEK00000 (this model has legacy support enabled)
* HID Indala ASR-620++ (No Longer Manufactured by HID)

*To simplify the process, you can purchase a DIY Doppelgänger Breakout Board which will reduce wiring complexity and provides voltage regulation and logic conversion for you. If you want to go the true DIY route, we recommend purchasing the following items:*

The following additional items are recommended to build a complete system:

| Item                                                        | Qty |
| ----------------------------------------------------------- | --- |
| SparkFun Thing Plus C                                       | 1   |
| Powerbank (Omni Mobile 25600mah recommended)                | 1   |
| Adhesive Standoffs 0.180" Height                            | 4   |
| 1.5' USB-C to USB-A Cable                                   | 1   |
| 5.5x2.1mm Power Cable (Male)                                | 1   |
| SparkFun Logic Level Converter                              | 1   |
| 22 awg Solid Core Wire (Six Color Pack)                     | 1   |
| 1" Outdoor Zip Tie Mounts and Zip Ties                      | 2   |
| 2.54mm 0.1" Pitch PCB Mount Screw Terminal Block Connectors | 1   |

Below are the wiring diagrams for each reader. As the RFID readers below output a 5V signal, the use of a logic level converter is required to adapt the signal to 3.3V.

*Note, you can use various ESP32's, the diagrams below are merely an example.*

![MaxiProx Wiring](https://github.com/optiv/doppelganger/blob/main/git_images/maxiprox_wiring.jpg)

![ICLASS SE Wiring](https://github.com/optiv/doppelganger/blob/main/git_images/iclass_se_wiring.jpg)

![Indala Wiring](https://github.com/optiv/doppelganger/blob/main/git_images/indala_wiring.jpg)

![SE Installation](https://github.com/optiv/doppelganger/blob/main/git_images/se_install.jpg)

![Indala Wiring](https://github.com/optiv/doppelganger/blob/main/git_images/indala_install.jpg)

## Getting Started with Doppelgänger

For setup purposes, I recommend using a computer to configure the device initially. Once the Doppelgänger has been configured to connect to a mobile device, there should be no need to use a computer again.

1) Apply power to the reader and ESP-32.
2) If the blue LED is illuminated, the device is in configuration mode. Connect to the **doppelgänger_XXXX** network using the default password **UndertheRadar**.
3) The Captive Portal should automatically launch. If it does not, navigate to <http://192.168.4.1/>.

**Captive Portal Menu Options:**

* **Configure WiFi** - Performs a scan of wireless networks.
* **Configure WiFi (No scan)** - Same as above, but without scanning for wireless networks.
* **Info** - Provides general information about the device, including temp, memory usage, build date etc. Note that the "ERASE WiFi Button" only clears stored wireless network credentials. It does not clear email configuration data. The only way to clear e-mail configuration data is through the web application.
* **Update** - OTA firmware update. To choose this option, use your web browser and open the Captive Portal (<http://192.168.4.1/>).
* **Restart** - Self-explanatory
* **Exit** - Self-explanatory

![WiFi Manager Menu.png](https://github.com/optiv/doppelganger/blob/main/git_images/wifimanager.jpg)

## Connecting Doppelgänger to a Mobile Device

Before selecting **Configure WiFi** in the captive portal, turn on your mobile device's **Personal Hotspot**.

**iPhone:**

* Ensure that you enable ***Maximize Compatibility*** in the ***Personal Hotspot*** menu.
* You must leave the Personal Hotspot menu open while scanning and connecting Doppelgänger to your device.
* If no wireless networks appear in the **Configure WiFi** menu, clicking **Refresh** at the bottom of the page will initiate a network scan. Doppelgänger is preconfigured to filter out weak wireless networks which should help reduce clutter in WiFi-dense areas.
* Connect to your Mobile Device's hotspot.
* Upon clicking the **Save** button, Doppelgänger will save the wireless configuration and reboot. Upon reboot, Doppelgänger will automatically attempt to connect to the assigned wireless network.
* Once connected: Open your web browser to <http://rfid.local/> to access the Doppelgänger web application.

**Android:**

* Not tested: The process will be similar to the iPhone instructions.

## Setting Up E-mail Notifications

If you want to enable e-mail notifications, navigate to the Notifications page on the Doppelgänger web application. Enter your SMTP credentials and recipient information. This data is stored on the internal flash storage and is not accessible from the SD Card/web application. The notification configuration can be wiped by using Doppelgänger's reset functionality from within the web application.

To send a text notification follow this schema:

```text
Verizon: 5551234567@vtext.com
AT&T: 5551234567@txt.att.net
Rogers: 5551234567@pcs.rogers.com
T-Mobile: 5551234567@tmomail.net
Google-Fi: 5551234567@msg.fi.google.com
Sprint: 5551234567@messaging.sprintpcs.com
Virgin Mobile: 5551234567@vmobl.com
```

## Reconnecting to Doppelgänger

Ensure that you have the Personal Hotspot menu opened on your iPhone before powering Doppelgänger back up (I am uncertain if Andriod devices operate in the same manner). Otherwise, Doppelgänger may not see your hotspot and will enter configuration mode. If this happens, you can either wait out the 120-second reset timer, in which Doppelgänger will reboot and look for the stored wireless network again or enter into the Captive Portal and make changes/restart the device manually.

## Web Application & Notifications

Here's a quick look at the web application for reference:

![WebApp.png](https://github.com/optiv/doppelganger/blob/main/git_images/webapp_view.jpg)

## Debugging

Should you want to dive deeper into what Doppelgänger is doing under the hood, You can connect to the device using the terminal or [PlatformIO/vscode](https://docs.platformio.org/en/latest/).

To connect to the device from the terminal:

```bash
ls /dev/tty.usb*
screen /dev/tty.usbserial-13440 115200
```

To connect to the device from PlatformIO/vscode: Open a PlatformIO project (this repository) and click the monitor button.

![Boot Process](https://github.com/optiv/doppelganger/blob/main/git_images/boot_process.jpg)
![Card Handling](https://github.com/optiv/doppelganger/blob/main/git_images/card_handling.jpg)

## Flashing the device

Doppelgänger can be flashed using PlatformIO plugin in VSCode

### Build and Upload the Filesystem

Attach the SparkFun board to your computer and click on the alien (PlatformIO) icon inside of VSCode. If you're using the IoT Redboard, you will not need to change the boot mode. If you're using the Thing Plus C, you may need to press the **BOOT** button before writing firmware / performing filesystem operations.

* Under **PROJECT TASKS -> Platform**, click **Build Filesystem Image**. This will create the LittleFS filesystem.
* Under **PROJECT TASKS -> Platform**, click **Upload Filesystem Image**. This will upload the filesystem to the IoT RedBoard. *Note, if you receive an error, it's likely that you have the serial monitor running. Close the serial monitor and try again.*

### Build and upload the Firmware

* Click the **Trashcan** on the lower ribbon of VSCode. This will **clean** the project.
* Click the **Checkmark** on the lower ribbon of VSCode. This will build the firmware.
* Click the **RightArrow** on the lower ribbon of VSCode. This will upload the firmware to the device. *You may need to press the boot button on the device.*

## Writing Captured Card Data

As part of the Doppelgänger eco-system, I have created [Doppelgänger Assistant](https://github.com/tweathers-sec/doppelganger_assistant). This tool is designed to make it easy to write captured card data with a Proxmark3. Below is a quick video demo of the usage:

[![Doppelgänger Assistant Demo](https://img.youtube.com/vi/RfWKgS-U8ws/0.jpg)](https://youtu.be/RfWKgS-U8ws)

## Credit / Special Thanks

Special thanks to the following folks:

Francis Brown - To this day, "RFID Hacking Live Free or RFID Hard" remains my favorite
conference talk. Watching that talk blew my mind as I left the military many years ago and started penetration testing. Truly inspirational!
Daniel Smith - For laying so much of the groundwork that has made all of these awesome tools possible.
