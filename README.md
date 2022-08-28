# Klipper printers
Repo to store printer settings and code to go from a clear install to a functional one

# Code from A to functional printer

Update Moonraker and gives permissions:

>cd ~/moonraker/scripts \
>./set-policykit-rules.sh \
>sudo service moonraker restart

# Add CAN network

> sudo nano /etc/network/interfaces.d/can0

in this file, put:

>auto can0\
>iface can0 can static\
>   bitrate 500000\
>   up ifconfig $IFACE txqueuelen 128

##Building CANBoot

>git clone https://github.com/Arksine/CanBoot\
>cd CanBoot

>make menuconfig

Processor model select STM32F072
Clock Reference select 8 MHz crystal , the default is OK
CAN pins select Pins PB8(rx) and PB9(tx)
CAN bus speed The CANBUS speed should be kept consistent according to your CAN configuration and klipper firmware configuration. Commonly 500000 and 250000
Other configurations can be kept as default and do not need to be modified. The specific configuration is shown in the figure below
Only keyboard operation is possible here, up and down keys to select the menu, Enter key to enter the menu or confirm, ESC to return to the previous page
SHT36/42 configuration as shown
After the configuration is completed, press the "Q" key, and then press the "Y" key to exit and save

>make

To find the device ID 

> ~/klippy-env/bin/python ~/klipper/scripts/canbus_query.py can0


Change in `toolhead.cfg` the `canbuss_uuid:` to the correct one for your device. Maybe the device is not recognize. Try to unplug and replug it 




# Sources
- https://www.klipper3d.org/CANBUS.html
- https://mellow.klipper.cn/#/advanced/canboot?id=%e6%9e%84%e5%bb%bacanboot%e5%bc%95%e5%af%bc%e5%9b%ba%e4%bb%b6
- https://github.com/Lecso11/My-printers/tree/V2.2089/My%20mods/Mellow%20FLY-SHT36%20mount
- https://www.youtube.com/watch?v=0XUWcFOhqM4

