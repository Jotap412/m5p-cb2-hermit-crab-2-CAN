# m5p-cb2-hermit-crab-2-CAN
Guide on how to configure CAN Bus on the Bigtreetech Manta M5P with a CB2 V1.0 board and a Hermit Crab 2 Tool Changer

List connected devices with:
```
lusb
```
The board should show as: "STMicroelectronics STM Device in DFU Mode"

Copy the device ID (in this case "0483:df11") and flash the device with the command:

```
make flash FLAHS_DEVICE=0483:df11
```

(Make sure that you input the correct device ID in the command)

References:
https://klipper.discourse.group/t/canbus-bridge-mode-configuration/6693
