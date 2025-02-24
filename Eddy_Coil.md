I tried to connect an Eddy Coil to the Hermit Crab 2

When I tried to run:

```
LDC_CALIBRATE_DRIVE_CURRENT CHIP=btt_eddy
```

I got the error:

```
Unable to obtain 'i2c_read_response' response
```

And the printer would shut down

![](/images/E1-Error.png)

After some hours of troubleshooting I found this thread:

https://klipper.discourse.group/t/manta-mp8-v2-shutdown-i2c-timeout/18892/1

The steps I took to make it work

<br>

### 1. Update MCU and HermitCrab2 versions of Klippy

I noticed that I have been updating the CB2 Klipper version but the Manta M5P and the HermitCrab2 Klipper versions were different

> The version of the software can be checked in the Mainsail Web Interface "MACHINE" tab

![](/images/E2-Version.png)

If the Versions do not match, follow the guide to update them

<br>

### 2. Bad Wiring

From the thread above that I checked, one common error is bad wiring

So I checked the Hermit Crab Manual:

![](/images/E3-HC2Manual.png)

In the schematic above, the SCL is on GPIO6 and de SDA on GPIO7

**Although, in the M5P official configuration file <ins>those pins are switched</ins>:**

![](/images/E4-HC2cfg.png)

In fact, in the I2C Bus used by the HermitCrab2 (i2c1b), the first pin (SCL) is GPIO6 and the second pin (SDA) is GPIO7:

![](/images/E5-HC2pins.png)

I tried switching the SCL and SDA wires on the probe and it began to work. It is now wired like this:

![](/images/E6-wiring.png)
