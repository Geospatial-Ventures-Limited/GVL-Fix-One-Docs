# Configuration

`GVL Fix One` reads from a **configuration file** at startup to determine what to do.

## Accessing Storage

* Plug the the device into a computer

* Hold power button to switch on

* On boot screen, **press any button**.

* A **USB drive** should show up on the computer

## Files

All files are stored at the **root of the SD card**.

* **Configuration File**: `gvl_config.txt`
* **MQTT over TLS**
    * Put the server CA certificate as `mqtt.crt`
	* Not needed for unencrypted MQTT

## Configuration Options

* Open `gvl_config.txt` with a text editor

Inside, there are multiple lines of `option=value` pairs.

Here's an example, details below.

```
nickname=gvl_test

wifi_ssid=myWifi
wifi_pass=hunter2

// 0: Rover, 1: Basestation
device_role=0

// 0: Wi-Fi, 1: Cellular, 2: No Comm.
comm_type=0

send_gga=1
use_mqtt=1

// Rover fix rate in Hz (1, 2, 5, or 10)
rover_refresh_rate=1

ntrip_addr=ntrip.data.gnss.ga.gov.au
ntrip_port=2101
ntrip_cred=username:password
ntrip_mountpoint=AUTO

mqtt_addr=test.mosquitto.org
mqtt_port=1883
mqtt_username=username
mqtt_password=password

```

* Make sure **there are no space before or after `=`**

* If an option is not present in the file, its value defaults to **0** or **empty string**

### device_role

|  Type  | Example |
|:------:|---------|
| Integer | `device_role=1` |

* 0: Rover mode

* 1: Basestation mode

### `nickname`

|  Type  | Example |
|:------:|---------|
| String | `nickname=gvl_test` |

* Device nickname for easy identification

* Included in MQTT message and logged files

### comm_type

|  Type  | Example |
|:------:|---------|
| Integer | `comm_type=1` |

* 0: Use Wi-Fi for network connection

* 1: Use Cellular for network connection

* 2: No comms, won't connect to networks.

### `wifi_ssid`

|  Type  | Example |
|:------:|---------|
| String | `wifi_ssid=GVL_Demo` |

* Name of the Wi-Fi Access Point

### `wifi_pass`

|  Type  | Example |
|:------:|---------|
| String | `wifi_ssid=hunter2` |

* Password for the Wi-Fi Access Point

### `ntrip_addr`

|  Type  | Example |
|:------:|---------|
| String | `ntrip_addr=example.com` |

* Address of the NTRIP server

* Can be URL or IP address

### `ntrip_port`

|  Type  | Example |
|:------:|---------|
| Integer | `ntrip_port=2102` |

* Port of the NTRIP server

### `ntrip_cred`

|  Type  | Example |
|:------:|---------|
| String | `ntrip_cred=username:password` |

* Username and password for the NTRIP server, separated by `:` symbol.

### `ntrip_mountpoint`

|  Type  | Example |
|:------:|---------|
| String | `ntrip_mountpoint=GVL_Nearest` |

* Mount point to use with the NTRIP server

* Used in **rover mode**

### `send_gga`

|  Type  | Example |
|:------:|---------|
| Integer | `send_gga=1` |

* Whether or not to send NMEA GGA sentence to NTRIP server in rover mode

* Required by some NTRIP servers to select a suitable correction source

### `base_password`

|  Type  | Example |
|:------:|---------|
| String | `base_password=123456` |

* Used in **Basestation mode**

### `base_mountpoint`

|  Type  | Example |
|:------:|---------|
| String | `base_mountpoint=GVL_Base` |

* Name of the NTRIP mount point to send data to

* Used in **Basestation mode**

### `base_x`, `base_y`, `base_z`

```
base_x=415365.781
base_y=-36584.062
base_z=687452.299
```
* Coordinates of the GNSS antenna

* Used in **Basestation mode**

### `use_mqtt`

|  Type  | Example |
|:------:|---------|
| Integer | `use_mqtt=1` |

* Whether or not to send real-time updates via MQTT

### `mqtt_addr`

|  Type  | Example |
|:------:|---------|
| String | `mqtt_addr=test.mosquitto.org` |

* Address of MQTT server

* Can be URL or IP address

### `mqtt_port`

|  Type  | Example |
|:------:|---------|
| Integer | `mqtt_addr=1883` |

* Port of MQTT server

### `mqtt_username`

|  Type  | Example |
|:------:|---------|
| String | `mqtt_username=gvl_user` |

* MQTT username

* Optional

### `mqtt_password`

|  Type  | Example |
|:------:|---------|
| String | `mqtt_password=123456` |

* MQTT password

* Optional

### `log_sd`

|  Type  | Example |
|:------:|---------|
| Integer | `log_sd=0` |

* Whether or not to save GNSS result to SD card

### `rover_rtcm`

|  Type  | Example |
|:------:|---------|
| Integer | `rover_rtcm=1` |

* Enable RTCM MSM7 output in rover mode

* Useful for postprocessing

    * 0: Disabled

    * 1: Enable RTCM output and stream it to the NTRIP caster

    * 2: Enable RTCM output and save to SD card only (skips the network connection)

### `rover_refresh_rate`

|  Type  | Example |
|:------:|---------|
| Integer | `rover_refresh_rate=1` |

* Rover position fix rate in Hz

* Valid values: `1`, `2`, `5`, `10`.

### `ntrip_reboot_sec`

|  Type  | Example |
|:------:|---------|
| Integer | `ntrip_reboot_sec=240` |

* Reboot device fi no NTRIP correction data is received for this many seconds

* Default: `240`

* Set to `0` to disable

### `enable_imu`

|  Type  | Example |
|:------:|---------|
| Integer | `enable_imu=1` |

* Enable raw IMU output on the GNSS module

## Cellular Options

These options apply when `comm_type=1` (Cellular).

### `cell_apn`

|  Type  | Example |
|:------:|---------|
| String | `cell_apn=internet` |

* Access Point Name (APN) for the cellular carrier

### `cell_pap_username`

|  Type  | Example |
|:------:|---------|
| String | `cell_pap_username=user` |

* PAP username for the cellular connection

* Optional, depends on carrier

### `cell_pap_password`

|  Type  | Example |
|:------:|---------|
| String | `cell_pap_password=pass` |

* PAP password for the cellular connection

* Optional, depends on carrier

### `iotopmode`

|  Type  | Example |
|:------:|---------|
| Integer | `iotopmode=0` |

* 0: LTE Cat M1
* 1: NB-IoT
* 2: Both (Auto Select)

