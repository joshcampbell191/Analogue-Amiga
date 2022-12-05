# Analogue Pocket - Commodore Amiga 500 - 0.0.5 Alpha

The Commodore Amiga 500 was a personal computer that replaced the well-loved Commodore C64 in the Commodore product line. It also was one of the many 68K personal computers that showed that this CPU was a powerhouse when integrated with great hardware beside it.

This is based on the Mister Github of the Amiga Mist project (Also known as the minimig) and the VexRISCV RISC-v chip for the Media Processing Unit (MPU) between the core and APF framework for floppy, hard drive and CDrom access.

## What can it do?
* Both 68K and 68020 CPUs
* Chip memory 512k, 1m, 1.5m and 2m
* Slow memory none, 512k, 1m, 1.5m
* Fast memory of none/2/4/8Mbyte for the 68000K CPU
* Fast memory of 16/32Mbyte for the 68020K CPU setup - Another 32Mbytes will be added soon
* AGA Chipset
* Turbo boot
* It can only read ADF disk images (Floppy disks). Writes will come soon with Hard Drive access.

## How to setup
* Place your ADF floppy images in the \asset\amiga\common folder
* Place the kickstart BIOS rom in the \asset\amiga\common folder (I'm using the 1.2 for now, but any original firmware rom will work - no encrypted BIOSes yet). Name it to kickstart.rom to autoload it
* Make sure that the \asset\amiga\Mazamars312.amiga\ Folder has the mpu.bin file - this is supplied and should already be there.
* When changing system configurations, you must select the "CPU reset" in the menu to apply the config.

## Is the best way to play this using the dock?

* Yes, as you can then fully use the Keyboard and mouse to interface many games and functions. Just make sure you select in the Port1/Port2 as Mouse/Joystick1 or Mouse/CD32 for mouse access

## Is there an emulated mouse while not connected to the dock?

* Yes, Press both the left and right triggers, and the dpad becomes the movement and the buttons are emulated on buttons A,B,X. However, they are as follows – B for the left click, A for the Right click and X for the middle. For me, it just felt better when in this mode but I will look at interaction menu to change this.
* Please note that you have to have the Port1/Port2 setup as Mouse/Joystick1 or Mouse/CD32 for the mouse to work

## Is there an emulated Keyboard?

* Not at this moment, This is up for the next build as I have not decided on the best way to do this yet.

## Can we write to floppy disks at this moment?

* No, I have the code ready, but I want to check it before releasing it and add double buffering for faster access.

## When are writable disks and Harddrives going to be working?

* Now that the framework for the MPU has been built, this is a matter of getting the C++ code working with the MPU and APF interface.

## Wait, you have another CPU in the FPGA???

* Yes, the MPU is a VexRISCV CPU configured with a small footprint to interface with the APF interface to the HPS bus currently in the MiSTer Amiga core.

Specs:
* Running at 74.2mhz (Same as the APF bus)
* Connected to the core via a 16bit HPS Bus 
* Two timers - one for interrupts and the other for user timing.
* Currently, 32K of memory/ram for the MPU's program (Will be set to 16K for a smaller footprint)
* A 2Kbyte swap buffer for both the APF and MPU to do transfers
* A separate GitHub for the MPU and the APF framework for other developers to use soon with documentation.

## I have selected a disk that is taking some time to load?

* So it could be due to the game loading still. That's what that excellent green indicator at the top left-hand side is for :-)
* Try only using one disk drive - I have found that some games don't like having more than one floppy drive.
* The double buffering, as I will use the APF target bus commands to transfer DMA data while processing data to the core simultaneously. Right now, these are two concurrent processes
* Analogue-supplied Dev Units can use the UART interface on the Dev Cart (Baud rate of 115200) to see what the MPU is doing with the debug logs.

## Why are some of the resolutions not correct?

* I need to see the standard resolutions to ensure the scaler will work correctly - Interlacing is one thing I need to build up.
* Due to memory access, the RTG resolutions will not work on this right now.

## I have game X that does not work!!!

* From the testing I have been doing, there are multiple configurations, bios and even ADF Images that you need to try. Hopefully, once I get both writing to floppy and the Harddrive access working, this will help with the current bugs. 
* The main goal of this project was getting an MPU Framework so external media can be accessed and giving developers some tools to help create more cores on the Pocket.

## Credits

* This source code is based on Rok Krajnc project (minimig-de1).
* Original minimig sources from Dennis van Weeren with updates by Jakub Bednarski are published on Google Code and the Community.
* ARM firmware updates and minimig-tc64 port changes by Christian Vogelsang (minimig_tc64) and A.M. Robinson (minimig_tc64).
* MiSTer project by Sorgelig (MiSTer) and the Community.
* TG68K.C core by Tobias Gubener.
* VexRISCV Team - https://github.com/SpinalHDL/VexRiscv
* Robinsonb5 for his time answering my questions on his 832 CPU - Tho I did not use this excellent-looking CPU, I was not able to get the C Compiler working 100% on my builds
* Boogerman for some coding questions - You still owe me on the use of my JTAG tho LOL
* Electron Ash, AGG23 as a beta tester.
* Terminator2k2 for his fantastic images for the bootup
* And many more, so please message me and I would happily add them to this!!
