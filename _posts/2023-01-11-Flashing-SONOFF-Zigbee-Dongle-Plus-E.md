I was able to succesfully flash [SonOff Zigbee dongle plus E](https://sonoff.tech/product/gateway-and-sensors/sonoff-zigbee-3-0-usb-dongle-plus-e/){:target="_blank"} with router firmware. Detailing the steps below, as I wasn't able to find a guide on how to do this.

#### Why you might need to flash firmware:
- upgrade
- to use a different (opensource) option
- convert a Zigbee coordinator into a Zigbee router (this was my use case)


Apparently, the [SonOff Zigbee dongle plus E](https://sonoff.tech/product/gateway-and-sensors/sonoff-zigbee-3-0-usb-dongle-plus-e/){:target="_blank"} acts as a very good router (I have just started using it as router and so far it's reliable).



Step 1:
Unscrew [SonOff Zigbee dongle plus E](https://sonoff.tech/product/gateway-and-sensors/sonoff-zigbee-3-0-usb-dongle-plus-e/){:target="_blank"}'s case. Will need to only unscrew the 2 screws which are on the side of the USB port. This is to get access to the boot button.

!PHOTO GOES HERE !

Step 2:
Download and install [minicom](https://packages.debian.org/sid/minicom){:target="_blank"}, how you download might be different based on the OS you are using.
For linux OS, run the below command:
```
sudo apt-get install minicom
```

Step 3:
Run the below command and make a note of all the devices that show up:
```
ls /dev/tty*
```
Sample output:
```
gmagal@masterrpi:~ $ ls /dev/tty*
/dev/tty    /dev/tty11  /dev/tty15  /dev/tty19  /dev/tty22  /dev/tty26  /dev/tty3   /dev/tty33  /dev/tty37  /dev/tty40  /dev/tty44  /dev/tty48  /dev/tty51  /dev/tty55  /dev/tty59  /dev/tty62  /dev/tty9
/dev/tty0   /dev/tty12  /dev/tty16  /dev/tty2   /dev/tty23  /dev/tty27  /dev/tty30  /dev/tty34  /dev/tty38  /dev/tty41  /dev/tty45  /dev/tty49  /dev/tty52  /dev/tty56  /dev/tty6   /dev/tty63  /dev/ttyAMA0
/dev/tty1   /dev/tty13  /dev/tty17  /dev/tty20  /dev/tty24  /dev/tty28  /dev/tty31  /dev/tty35  /dev/tty39  /dev/tty42  /dev/tty46  /dev/tty5   /dev/tty53  /dev/tty57  /dev/tty60  /dev/tty7   /dev/ttyprintk
/dev/tty10  /dev/tty14  /dev/tty18  /dev/tty21  /dev/tty25  /dev/tty29  /dev/tty32  /dev/tty36  /dev/tty4   /dev/tty43  /dev/tty47  /dev/tty50  /dev/tty54  /dev/tty58  /dev/tty61  /dev/tty8
```

Step 4:
Keeping the `boot` button pressed connect it to the computer's USB port. Only steady red LED will glow

!PHOTO TO SHOW THE BOOT BUTTON!

Step 5:
Now, run the same command as Step 3. This time we will take a note of the serial device i.e. [SonOff Zigbee dongle plus E](https://sonoff.tech/product/gateway-and-sensors/sonoff-zigbee-3-0-usb-dongle-plus-e/){:target="_blank"}:
```
ls /dev/tty*
```
Sample output:
```
gmagal@masterrpi:~ $ ls /dev/tty*
/dev/tty    /dev/tty11  /dev/tty15  /dev/tty19  /dev/tty22  /dev/tty26  /dev/tty3   /dev/tty33  /dev/tty37  /dev/tty40  /dev/tty44  /dev/tty48  /dev/tty51  /dev/tty55  /dev/tty59  /dev/tty62  /dev/tty9
/dev/tty0   /dev/tty12  /dev/tty16  /dev/tty2   /dev/tty23  /dev/tty27  /dev/tty30  /dev/tty34  /dev/tty38  /dev/tty41  /dev/tty45  /dev/tty49  /dev/tty52  /dev/tty56  /dev/tty6   /dev/tty63  /dev/ttyACM0
/dev/tty1   /dev/tty13  /dev/tty17  /dev/tty20  /dev/tty24  /dev/tty28  /dev/tty31  /dev/tty35  /dev/tty39  /dev/tty42  /dev/tty46  /dev/tty5   /dev/tty53  /dev/tty57  /dev/tty60  /dev/tty7   /dev/ttyAMA0
/dev/tty10  /dev/tty14  /dev/tty18  /dev/tty21  /dev/tty25  /dev/tty29  /dev/tty32  /dev/tty36  /dev/tty4   /dev/tty43  /dev/tty47  /dev/tty50  /dev/tty54  /dev/tty58  /dev/tty61  /dev/tty8   /dev/ttyprintk
```
If you notice, we see the USB device - `/dev/ttyACM0`. This will be needed for configuring [minicom](https://packages.debian.org/sid/minicom){:target="_blank"}


Step 6: Run the below command to start [minicom](https://packages.debian.org/sid/minicom){:target="_blank"}

```
sudo minicom -s -c on
```
This will pop-up below screen in the terminal.
!PHOTO here!

You can navigate the screen using keyboard arrows and choose specific suboption choose the alphabet next to it.
Below are the things that needs to be configured before we can flash the device:
1. Filenames and paths: Provide the directory path where you have downloaded the new firmware which you want to flash
!Photo here!

2. File transfer protocols: XMODEM should be enabled (it's enabled by default). This is how it should look
! Photo here !

3. Serial port setup: This is the place where we specify our Serial Device (which we obtained in Step 5 above). The baud rate
should be 115200 (default)
!Photo here !

4. Save the Setup as df1: Save our configuration, so that next time the settings are saved
!Photo here !

5. Exit: Exit from the configuration screen. This should take to the command screen
!Photo here !

Step 7: Now press `1` on the keyboard, you should see something like below, the upload connection is established to the USB device:
!Photo here !

Step 9: Now press `control` and `a` together, leave it and press `z` on your keyboard, this should open up the options and you can `s` is used for sending file to the device
!Photo here!

Step 10: Press `s`, you should see options like below:
!Photo here! 

Step 11: We need to choose `xmodem` protocol. Use keyboard arrow to navigate to `xmodem` and hit `return` on your keyboard. This should open up a dialog inside terminal showing all the files available inside the directory which we had configured in Step 6 (under 1).
!Photo here!

Step 12: Using keyboard arrow key navigate to the firmware file and hit space bar to choose that file, followed by return. This should start the upload
process and you should see something like:
!Photo!

Step 13: Now disconnect [SonOff Zigbee dongle plus E](https://sonoff.tech/product/gateway-and-sensors/sonoff-zigbee-3-0-usb-dongle-plus-e/){:target="_blank"} from your computer

Step 14: Screw back the case and plug it into any USB outlet with 5V DC (minimum 1Amp current). You have the router ready in pairing mode.


Step 15: Use Homeassistant or zigbee2mqtt or whatever software you use to pair the new router with your zigbee coordinator





#### What is Zigbee
Zigbee is a wireless communication standard used for the creation of personal area networks (PANs) with low-power digital radios, such as those used in home automation, medical device data collection, and other low-power IoT devices.
It operates in the 2.4 GHz frequency band and is designed to be a low-cost, low-power, and secure mesh networking solution.

Zigbee Coordinator:
In a Zigbee network, the Zigbee coordinator is the device responsible for establishing and maintaining the network. It acts as the central hub, creating the initial network and managing network parameters, such as security keys, network address assignment,
and network topology.

Zigbee Router:
Zigbee router is a device that serves as an intermediary between the coordinator and other devices on the network. Routers help extend the range of the network by forwarding messages and data between devices, and also help to reduce the workload
on the coordinator by allowing it to manage fewer devices directly.