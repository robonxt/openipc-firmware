## OpenIPC Install ##    

#### June 8th, 2018 ####

#### Version 0.2.6.1

### Full Disclosure ###
- OpenIPC for Wyze V1 is forked from _fang-hacks_ and is based on a proprietary Xiaomi firmware (FIRMWARE_660R.bin) with implementations allowing the end user to take full control of their Wyze camera.
- At this time OpenIPC is not a 100% completely open source project as we rely upon the chinese base firmware at the moment to execute our payload (install method).
- We do not have intentions to rewrite low level boot code and drivers for this camera model, instead we provide end users the ability to mitigate risk by gaining full root control.
- Source code repositories for all added binaries will be added to the project shortly (snx_rtsp_server/dropbear). The inherent risk of a chinese base firmware can now be fully mitigated.

#### Notable Changes from fang-hacks ####
  - Roadmap for OpenIPC Fork
  - Wifi setup via SDcard script
  - Includes downgrade firmware
  - Audio on RTSP as a toggle option
  - Includes rtsp scanner and openipc scanner

### Known Issues: ###
- Full HD (1080p) not supported. 1600x900 is the maximum resolution.
- https://github.com/EliasKotlyar/Xiaomi-Dafang-Hacks/issues

### Repository Folder Stucture ###
  - firmware_mod/ - openipc sdcard firmware root structure and files
  - firmware_original/ - original wyzecam stock firmware
  - releases/ - openipc modified wyzecam firmware bin files and v1 release image
  - wyze-firmware-unpacker/ - tools to modify and extract wyzecam firmware

### Installation Instructions Wyze V1: ###
1. Download and install [Etcher](https://etcher.io) or [Win32 Disk Imager](https://sourceforge.net/projects/win32diskimager/)
2. Write the openipc_vX.X.X.img to your SDcard
3. Open the SDCard and edit the files .wifissid and .wifipasswd to match your network
4. Flash the firmware to the camera:
    - Hold down the setup button for 10 seconds BEFORE connecting power
    - With button still depressed, plug in power to the camera while continuing to hold for another 10 - 12 seconds.
    - Release the button when the connection light blinks continually.
    - Press the button again and you should hear a Chinese voice prompt if successful.
5. Remove SDcard and reboot camera and reinsert after boot until you hear "click click".
6. Repeat Step 5 until you hear "click click".
7. Run openipscan.sh or openipscanwin.sh if you're on windows/mac and find the IP address of your new OpenIP Camera. Note: MAC address will be changed to c0:6d:1a*
8. Proceed to the status web page and apply the hacks. http://[discoveredipaddress]/cgi-bin/status 
9. RTSP stream (when enabled), rtsp://xxx.xxx.xxx.xxx:8554/unicast

NOTE: of you get a 404 error with a flashing blue led, Remove the sdcard and reinsert it. Shortly after thst the camera will go "click click" again. Proceed to the link now

Congratulations! Welcome to OpenIPC.

### Upgrade existing OpenIPC install V1 (script) ###
1. Download or clone the repo and cd into it
2. Run ./update.sh openipciphere

### Upgrade existing OpenIPC Install: ###
1. Download and install [Etcher](https://etcher.io) or [Win32 Disk Imager](https://sourceforge.net/projects/win32diskimager/)
2. Write the openipc_vX.X.X.img to your SDcard
3. Open the SDCard and edit the files .wifissid and .wifipasswd to match your network
4. Reboot camera and reinsert SDcard after boot until you hear "click click".


### Connection Details: ###
    - RTSP: rtsp://[discoveredipaddress]/unicast Port 554
    - SSH: root/openipcam Port 22 (earlier versions password is ismart12)

### Scripts ###
    - update.sh - takes Wyze IP as first argument (updates via scp)
    - openipscan.sh - scans for openip.cam mac address with nmap

### Revert to Wyze firmware ###
    - https://wyzelabs.zendesk.com/hc/en-us/articles/360024852172-Release-Notes-Firmware

#### Build release image with dd ####
    - dd if=/dev/sdx of=~/openipc_v0.2.x.img bs=1 count=262144000


### Changelog: ###

#### Version 0.2.6.1 - Wyze All ####
    - Added stock firmware for wyzecamv2 and wyzecam pan.
    - Removed built images for wyzecamv2.
    - Added instructions on how to create proper installation sdcard for V2

#### Version 0.2.6 - Wyze All ####
    - Combined sdcard image for Wyze V1 and V2.
    - Fixed IR Support on Wyze V2..

#### Version 0.2.5 - Wyze V2 ####
    - Support for Wyze V2. **No longer supporting Wyze V1.**
    - HTML5 Web Interface
    - Fork from dafang-hacks - https://github.com/EliasKotlyar/Xiaomi-Dafang-Hacks
    - Support for Home Assistant, RTSP Authentication and MJPEG Streaming

#### Version 0.2.4 - Wyze V1 ####
    - RTSP configuration page with settings for rotate, mirror, flip, resolution, etc.
    - RTSP authentication is now possible
    - Crontab watchdog to reboot RTSP script
    - Revert to original Wyze firmware instructions
    - SCP update script from shell to camera


#### Version 0.2.3 ####
    - Added Audio on RTSP control to Web interface
    - Updated README for more clear instructions


Thanks to [EliasKotlyar](https://github.com/EliasKotlyar) for [Xiaomi-Dafang-Hacks](https://github.com/EliasKotlyar/Xiaomi-Dafang-Hacks) and @Datbit128 for help building the Wyze V2 CFW. 
Thanks to [samtap](https://github.com/samtap/) for [fanghacks](https://github.com/samtap/fanghacks) used as the base for OpenIPC. Thanks to [joeand37](https://github.com/joeand37) for inspiration. Thanks to the various other developers on the fanghacks page who cross-compiled some of the binaries.
