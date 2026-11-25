## Intro ##
This respository is a port of the standard Arduino CameraWebserver demo for the esp32 board to run within the ESP-IDF environment. It also adds support for Nulllab's esp32s3-cam board layout. I made this to familiarize myself with the wifi and camera componenets of the ESP-IDF environment and am releasing it to the public to help any others in a similar position.

## Usage ##

### Configuration ###
To start off be sure to set the target for your project using
```bash
idf.py set-target esp32s3
```

The current config is consistent with the Nulllab esp32s3-cam board with 
 * 8mb psram flash 
 * octal style memory

if your system uses a different flash size or quad memory style be sure to change the config using
```bash
idf.py menuconfig
```
and navigating to:
* Component config -> ESP PSRAM -> Suport for external, SPI-connected RAM -> SPI RAM config -> Mode (QUAD/OCT)
* Serial flasher config -> Flash size

In `wifi_utils.h`, enter your wifi ssid and password into the corresponding macros.

Before running be sure the macro in `myCamServer.c` corresponding to your board is uncommented and all others are commented out.

### Dependencies ###
The program should run out of the box in the ESP-IDF environment without any extra installation. However, newer users should note that the camera and jpeg dependencies were pre-installed into the `managed_components` folder using 
```bash
idf.py add-dependency "espressif/<package-name>"
```
for both components. Any fresh folders for similar projects would need to do the same to install the dependency.

### Running ###
To run the code you will need the name of the usb port your board is connected to. To find that name, first plug in your board then run
```bash
sudo dmesg | grep tty
```

Then to build and run the code do
```bash
idf.py -p /dev/<your-port-name> flash monitor
```

If all goes well you should see a message similar to
```
I (2936) wifi station: got ip:192.168.4.35
I (2936) app_httpd:: Starting web server on port: '80'
```
To access the server type `http://<ip_address>:<port_num>` into a browser. Click Start Stream and you should get continuous output from your camera!
