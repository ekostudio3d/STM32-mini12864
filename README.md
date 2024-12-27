# <p align="center">STM32-mini12864</p>

![Image](https://github.com/ekostudio3d/STM32-mini12864/blob/main/Images/mini_lcd_12864.jpeg)

[1. What is this](#1-what-is-this)  
 
[2. A solution](#2-a-solution)

[3. Firmware Compilation](#3-firmware-compilation-)  

[4. Board in DFU mode](#4-board-in-mode)  

[5. Find and add serial number](#5-find-and-add-serial-number)  

[FAQ](#faq) 

##Flashing and Configuration Guide

###If you are here is because you have received a board for your small LCD12864 panel from your VORON kit, don't worry this file will guide you step by step on how to flash and configure correctly your board to make your display work properly, Thank you for being here!

### Please read in the order presented on this page.

### 1. What is this?

This is a small adapter board dedicated to controlling a [FYSETC Mini 12864 Display](https://github.com/FYSETC/Mini-12864-Panel) included in the kit. It's intended to run the [Klipper](https://github.com/KevinOConnor/klipper) firmware.

### 2. A solution

It is a solution to reduce the amount of cables going from the display to the VORON kit. You will not need flat cables, you can connect directly from the STM32-mini12864 board behind the display to your PI controller via a USB type C cable.

# Setup Guide

### 3. Firmware Compilation

 - Login to your PI via SSH connection (This can be in [PuTTY](https://www.putty.org/) / [MobaXterm](https://mobaxterm.mobatek.net/) programs).

![Image](https://github.com/ekostudio3d/STM32-mini12864/blob/main/Images/cap1.png)

 - Enter the following commands to prepare the configuration
    ```bash
    cd klipper
	make menuconfig
	```
	
![Image](https://github.com/ekostudio3d/STM32-mini12864/blob/main/Images/cap2.png)

 - Configure the board firmware as follows
 
![Image](https://github.com/ekostudio3d/STM32-mini12864/blob/main/Images/cap3.png)
 
  - We will need to reduce space for the compilation, for this step go to this checkbox to uncheck some options
 
![Image](https://github.com/ekostudio3d/STM32-mini12864/blob/main/Images/cap6.0.png)
  
 - We will only leave these options enabled. Press `Q` on the keyboard to save and exit the settings 
 
![Image](https://github.com/ekostudio3d/STM32-mini12864/blob/main/Images/cap6.1.png)

 - Note that when switching between MCU architectures it is important to run `make clean` before `make`. This avoids strange compilation errors.
    ```bash 
    make clean
	make
    ```
	
![Image](https://github.com/ekostudio3d/STM32-mini12864/blob/main/Images/cap4.png)
 
### Generate firmware that matches the current klipper version.

### If the progress bar reaches 100%, it means the burning is complete, please ignore the displayed error

![Image](https://github.com/ekostudio3d/Klipper-Expander/blob/main/Images/img19.png)
 
### 4. Board in DFU mode

![Image](https://github.com/ekostudio3d/STM32-mini12864/blob/main/Images/cap20.jpg)

### You need a jumper to short the BOOT0 pins, connect the usb cable and press the RESET button, remove the jumper and the board should remain in DFU mode.

![Image](https://github.com/ekostudio3d/STM32-mini12864/blob/main/Images/stm32_mini_12864.jpeg)

### To perform this check, type the command `lsusb` and a device in DFU mode should appear.

    lsusb
![Image](https://github.com/ekostudio3d/STM32-mini12864/blob/main/Images/cap5.png)

 - Now flash the firmware with the following command make flash `FLASH_DEVICE=0483:df11`, the firmware was successfully flashed, ignore the error that appears at the end
    ```bash
     make flash FLASH_DEVICE=0483:df11
    ```

![Image](https://github.com/ekostudio3d/STM32-mini12864/blob/main/Images/cap7.png)

### The firmware was successfully flashed, ignore the error that appears at the end

![Image](https://github.com/ekostudio3d/STM32-mini12864/blob/main/Images/cap8.png)

## Mainsail / Fluidd configuration

### Add this file [Klipper-mini12864.cfg](https://github.com/ekostudio3d/STM32-mini12864/blob/main/Configure/klipper-mini12864.cfg) to your configuration by uploading a new file.

![Image](https://github.com/ekostudio3d/STM32-mini12864/blob/main/Images/cap9.png)

## Find and add serial number

It is important to know the serial number of our board to be able to include it in the file that we have just included in our configuration, with the command `ls /dev/serial/by-id/*` you can find the serial number of the klipperExpander boar. After completion `ls /dev/serial/by-id/*` should return a device begining with `/dev/serial/by-id/usb-Klipper_stm32f042x6...` 
 
    ls /dev/serial/by-id/*
![Image](https://github.com/ekostudio3d/STM32-mini12864/blob/main/Images/cap10.png)

### Now, copy and paste this serial into the file Klipper-mini12864 in the line `serial`.

![Image](https://github.com/ekostudio3d/STM32-mini12864/blob/main/Images/cap11.png)

### Now include the created configuration to your main file `printer.cfg`.
    ```bash
    [include Klipper-mini12864]
    ```
![Image](https://github.com/ekostudio3d/STM32-mini12864/blob/main/Images/cap12.png)

# <p align="center">`KILL BUTTON error`</p>

![Image](https://github.com/ekostudio3d/STM32-mini12864/blob/main/Images/cap13.png)

###Don't worry if you get this error in your interface, just remove the `!` sign that appears in the `kill_pin` line in the `Klipper-mini12864` file.

![Image](https://github.com/ekostudio3d/STM32-mini12864/blob/main/Images/cap14.png)

## FAQ

###Join our Discord and WeChat groups to receive after-sales support.

 <br/><img src=https://github.com/Lzhikai/SIBOOR-Voron-2.4-AUG/blob/main/Images/DISCORD.jpg width="1080"/><br/> 
 
 ## Links
- SIBOOR Official Discord: [https://discord.gg/tDe55eYx)
- VORON Official Website: [https://vorondesign.com/](https://vorondesign.com/)
- Klipper Official: [https://www.klipper3d.org/](https://www.klipper3d.org/)
- BTT Official: [https://github.com/bigtreetech](https://github.com/bigtreetech)