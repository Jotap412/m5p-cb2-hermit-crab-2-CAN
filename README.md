# m5p-cb2-hermit-crab-2-CAN
Guide on how to configure CAN Bus on the Bigtreetech Manta M5P with a CB2 V1.0 board and a Hermit Crab 2 Tool Changer

The Biqu / Bigtreetech documentation is lacking 

## 1. Initial Setup

<br/>

1. Plug in the CB2 module on the Manta board and flash the System image on the CB2 following the official guide:

  https://bttwiki.com/CB2.html#flashing-the-system

  > I flashed the system onto the eMMC (internal memory of the board), and avoided the use of a SDCard, but either option is valid. 
  
  <br/>

2. Configure the Wi-Fi connection or plug in an ethernet cable to the board

  https://bttwiki.com/CB2.html#using-ethernet\

  <br/>

3. Connect to the CB2 using SSH

  https://bttwiki.com/CB2.html#ssh-connect-to-device

  > Alternatively use Putty to establish the SSH connection, however I found the recommended software easier to use.

  Use the default login credentials:

```
login as: biqu
password: biqu
```

![](/images/1-SSH.png)

<br/>

## 2. Flashing the MCU - Manta Controller Board

<br/>

By now you should be able to connect to the CB2 via SSH

The MCU needs to be flashed with the USB to CAN bridge

1. Change directory to the klipper folder

```
cd klipper/
```

2. Enter the configuration menu

```
make menuconfig
```

![](/images/2-makemenuconfig.png)


3. Chose the correct options according to the MCU board following the official guide for the board **<ins>EXCEPT</ins> for the "Communication Interface"**


![](/images/3-MCU-config.png)


**The "Communication Interface" should be set to <ins>"USB to CAN Bus Bridge"</ins>**

**The "CAN Bus interface" should be set to <ins>the correct PIN for the board</ins>**

> To check which PINs the CAN interface should be set to, see the official .cfg file of the board on GitHub
> ![](/images/4-MCU-CAN-cfg.png)

4. Exit configuration menu pressing "q" and then "y" to save changes

5. Compile the firmware with the command

```
make
```

6. Put the Manta board in boot mode
   - Press and hold the BOOT0 button
   - Press and release the RESET button
   - Release the BOOT0 button
  

![](/images/5-BTNs.png)


7. Check if the Manta board is ready by listing connected devices with:

```
lsusb
```

The board should show as: "STMicroelectronics STM Device in DFU Mode"

8. Copy the device ID (in this case "0483:df11") and flash the device with the command:

```
make flash FLASH_DEVICE=0483:df11
```

> Make sure that you input the correct device ID in the command

If it promps for the sudo password, enter your password, default is "biqu"

9. Press and realease the "Reset" button on the board, or power cycle the hardware

10. Check if the CAN Bus network is visible with the command


```
ifconfig
```

You should see a network named "can0"

If you type the command "lsusb" again you should see a CAN Adapter

> The command to list Serial Devices "ls /etc/serial/by-id/" will not show the MCU since it is now recognized as a CAN Device instead of a Serial Device. In Klipper, the .cfg file must be changed to recognize the [mcu] by "canbus_uuid:" instead of "serial:"

<br/>

## 3. Configuring Klipper - printer.cfg

<br/>

By now


Run the command
```
~/klippy-env/bin/python ~/klipper/scripts/canbus_query.py can0
```
And copy the "canbus_uuid" of the Klipper device, this is the ID of the MCU




11. 

References:
https://klipper.discourse.group/t/canbus-bridge-mode-configuration/6693
https://klipper.discourse.group/t/canbus-query-py-not-returning-ebb36s-uuid-setup-pi-4-octopus-v1-1-ebb36-v1-2/8464
~/klippy-env/bin/python ~/klipper/scripts/canbus_query.py can0
