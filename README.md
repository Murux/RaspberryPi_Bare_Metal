RaspberryPi_Bare_Metal
======================

Bare Metal experiments with Raspberry pi

I am using Linux Mint 17 as operating system for my tasks.

*Stands for userspecific input*
// Stands for my thoughts, why I do something a specific way 
"" Stands for commands for your terminal

1. Preparations

For compiling the programmed C-code, I used arm-linux-gnueabihf-gcc, like proposed from the official Raspberry pi site.

To get started, create a new folder for you project and open a terminal inside it.
Now get the sources with 
"git clone https://github.com/raspberrypi/tools".
Now it's usefull to add the path in your .bashrc with 
"export PATH=$PATH:/home/*PathToYourDirectory*/tools/arm-bcm2708/gcc-linaro-arm-linux-gnueabihf-raspbian/bin" (on 64-Bit-Sytems it's "gcc-linaro-arm-linux-gnueabihf-raspbian-x64")
so that the path is set up from booting your PC. It's recommended to restart your PC now, or you have to type your "*export PATH...*" into each new terminal you start. You can check if everything worked by simply typing "arm-linux-gnueabihf-gcc" into your terminal. If it complains about a missing input file, it works.

// For testing purposes, you can try the blinking_led.c from here. I got it from 
// http://www.valvers.com/open-software/raspberry-pi/step01-bare-metal-programming-in-cpt1/
// and it gives an actual feedback through it's blinking LED (surprise)

You are able to compile you C-files to .elf-files now. To do this, change directory with your terminal to the position of the C-file and type 
"arm-linux-gnueabihf-gcc -mfpu=vfp -mfloat-abi=hard -march=armv6zk -mtune=arm1176jzf-s -nostartfiles *YourCFile.c* -o *YourOutputName.elf*"
into your terminal. You should have a .elf-file in your directory.

In the next step, we want to create a .img-file out of our .elf-file. The arm-linux-gnueabihf-gcc doesn't seem to have the possibility to objcpy, so I have installed gcc-arm-linux-gnueabi with 
"sudo apt-get install gcc-arm-linux-gnueabi". 

// Why didn't I only use gcc-arm-linux-gueabi? The compilation of the C-file had an Collect2 error, which is a linking // problem. When I find the reason for that, this README-file will be updated and the preparations hopefully a bit 
// easier :) 

If the installation is finished, simply type 
"arm-none-eabi-objcopy *YourElfFile*.elf -O binary *YourOutputName*.img"
in your terminal and you have your own .img-file.

To start your program, take your Boot-SD-Card of your Raspberry pi and copy your .img-file on it. After that, you open the config.txt and change the entry 
"kernel=kernel.img" to "kernel=*YourImgFile*.img".
If you start your Raspberry pi, your .img-file will be executed without an OS behind it.

sources:
http://www.raspberrypi.org/documentation/linux/kernel/building.md
http://www.valvers.com/open-software/raspberry-pi/step01-bare-metal-programming-in-cpt1/

2. Experimenting
First steps with http://www.valvers.com/open-software/raspberry-pi/step01-bare-metal-programming-in-cpt1/
//ToDo



3. (Probably) Failed approaches

- Qemu
Installation with 
http://xecdesign.com/qemu-emulating-raspberry-pi-the-easy-way/

// A good description to get a virtual Raspberry pi. The two problems with that simulation are                         // the probably not correct simulated hardware and a DHCP-network-problem on my side, so that I couldn't get a 
// ssh-connection to the Rasperry pi  


