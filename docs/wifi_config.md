# GVL Fix One: Change Configuration

`GVL Fix One` reads from **configuration files** at startup to determine what to do.

## Accessing Storage: USB Cable

* Plug the the device into a computer
* Hold power button to switch on
* On the boot screen, **press any key**.
* A **USB drive** should show up on the computer

## Accessing Storage: SD Card

* Disassemble the device and remove the SD card.
* Use a card reader to mount the card on PC

## Files

All files are stored at the **root of the SD card**.

* **Configuration File**: `gvl_config.txt` 

## Configuration Options

* Open `gvl_config.txt` with a text editor

Inside, there are multiple lines of `option=value` pairs such as below:

```
wifi_ssid=myWifi
wifi_pass=hunter2

// 0: Rover, 1: Basestation
device_role=0

// 0: Wi-Fi, 1: Cellular, others: No Comm.
comm_type=0

nickname=gvl_test

.....
.....

```

## Set up for Wi-Fi

Add (or edit) the following lines to match the smartphone hotspot.

```
comm_type=0
wifi_ssid=name
wifi_pass=password
```
* Make sure **there are no space before or after `=`**

## Set up for Cellular

Add (or edit) the following lines:

```
comm_type=1
cell_apn=eapn1.net (optional, delete this if unused)
cell_pap_username=Geospati (optional, delete this if unused)
cell_pap_password=Geospati (optional, delete this if unused)
```

* Make sure **there are no space before or after `=`**
* Add cellular APN and PAP credentials if specified by your cellular service provider, otherwise delete the lines.

## Reboot

* Save the configuration file

* Hold power button to switch off then on again

* Device should boot using new settings.
