# m5p-cb2-hermit-crab-2-CAN
Guide on how to configure CAN Bus on the Bigtreetech Manta M5P with a CB2 V1.0 board and a Hermit Crab 2 Tool Changer

The Biqu / Bigtreetech documentation is lacking 

## Initial Setup
<br/>

1. Plug in the CB2 module on the Manta board and flash the System image on the CB2 following the official guide:

  https://bttwiki.com/CB2.html#flashing-the-system

  I flashed the system onto the eMMC (internal memory of the board), and avoided the use of a SDCard, but either option is valid.<br/><br/>
<br/>
<br/>
2. Configure the Wi-Fi connection or plug in an ethernet cable to the board

  https://bttwiki.com/CB2.html#using-ethernet
<br/>
<br/>
3. Connect to the CB2 using SSH

  https://bttwiki.com/CB2.html#ssh-connect-to-device

  Alternatively use Putty to establish the SSH connection, however I found the recommended software easier to use.
<br/>
<br/>
## Flashing the MCU - Manta Controller Board



List connected devices with:
```
lsusb
```
The board should show as: "STMicroelectronics STM Device in DFU Mode"

Copy the device ID (in this case "0483:df11") and flash the device with the command:

```
make flash FLASH_DEVICE=0483:df11
```

(Make sure that you input the correct device ID in the command)

If it promps for the sudo password, enter your password, default is "biqu"

Press and realease the "Reset" button on the board

References:
https://klipper.discourse.group/t/canbus-bridge-mode-configuration/6693
https://klipper.discourse.group/t/canbus-query-py-not-returning-ebb36s-uuid-setup-pi-4-octopus-v1-1-ebb36-v1-2/8464
