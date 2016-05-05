# Programming Photon's Particle - Beginner's Guide

<img src="https://raw.githubusercontent.com/spark/hardware-libraries/master/CAD/Photon.jpg" alt="Photon" height="200" align="right"/>

First - congratulations for your choice on selecting [Particle](https://www.particle.io)'s Internet-Of-Things boards! Both the [Photon](https://www.particle.io/prototype#photon) (Wi-Fi) and [Electron](https://www.particle.io/prototype#electron) (GSM cellular) are a great option for beginners!

You can even call them the WiFi or Cellular equivalent of the [Arduino&copy;](www.arduino.cc)!

With very little development effort both boards allow you to build connected (to the Internet) devices and have them push data out and consume data in. Aside from the device API there is also cloud API which lets you consume and use that data and do many wonderful things.

TL;DR? If you want you can skip the overview and go straight to the [The Guide](#the-guide) !

## Overview

In this guide we'll be focusing on the Photon device. Most of the instructions apply to the Electron too.

You can find the official documentation at https://docs.particle.io/guide/getting-started/start/photon/ but in case you already have some coding experience you might find it somewhat lacking. Most of Particle's documentation is written with Mac users in mind and if you happened to have a PC things may seem overly complicated. Hence this guide and the goal to keep them simple!

### "The KISS Principle" or "Can I use NOTEPAD as my editor?"

Isn't it surprising how often we get carried away in our desire to make it nice, and pretty, and full-featured, and it just ends up complicated? Let's Keep It Simple!

The Photon is awesome in providing simplicity for doing small projects! Developing for it can also be as simple! :)

The goals of this guide are to provide you with a very basic development environment, and where you can have your first program up and running in minutes. No complicated drivers installation. Very few (one!) prerequisites to install!  No special editors.

Yup! You read that right - you can use Notepad as your editor if you wish! 

It really is that simple! :-)

# Photon, development and IDE options

You may have searched the internet already and may have [found](https://www.sparkfun.com/news/1907) that there are essentially 3 choices when selecting your IDE and development environment. 

Here they are again in order from simplest to most complicated:

  - All-online, where everything happens over the web and in a browser
    * Claim your device and configure its WiFi (with your cell phone - no computer required) - see [instructions](https://docs.particle.io/guide/getting-started/start/photon/#connect-your-photon)
    * Use [Particle's Web Editor](https://build.particle.io/)
    * Push new firmware to your Photon from the web (online update)

  - Edit locally, compile online
    * Do the initial WiFi setup of your device via USB cable from your computer (or you can still claim your device with just your cell phone)
    * Use your favorite editor to write your code (and if NOTEPAD happened to be your choice - that's fine!)
    * compile online - save yourself setting up the whole compiler chain and instead push your source files to Particle's servers which will compile them for you and give you the binary back
    * Upload your compiled binary via USB cable

  - Do everything offline - see "simple" guide at https://community.particle.io/t/local-development-and-gdb-debugging-with-netbeans-a-step-by-step-guide/7829/2
    * Initialize, claim and configure WiFi for your Photon (use either method - cell phone or computer/USB cable)
    * Install ARM-GCC toolchain 
    * Use JTAG for hardware debugging (ST-Link/ST-Link V2) with NetBeans or Eclipse

# The Guide

This guide presumes that you like using your favorite editor and want to have all of your source code stored locally on your computer.

## Keep It Simple!

For simplicity we'll stay away from USB cables and drivers. We'll use the cloud and web for as much as possible and just keep our favorite editor!

Here is an overview of the process:
  * Claim and initially configure your device (using phone, or see below for doing that using your computer and a USB cable)
  * Install "The Prerequisite" software - [Node.JS](nodejs.org) with Particle's Command-Line Interface (CLI) which runs on top of NodeJS
  * Edit locally (Yup, NOTEPAD is just fine!) - you can use one of the examples from this repository as a start
  * Use Particle's online compiler
  * Push updated firmware to your device via the web


## The slightly more reliable and yet still simple way

Unfortunately registering your device using just your tablet or cell phone isn't always as simple as it sounds. And what if your WiFi is somewhat picky, maybe too protected, add some networking/dhcp/firewall/etc issues in the mix, etc and suddenly getting those updates pushed to your Photon just don't work?

A USB cable is your solution!

Here is how the process looks in summary:

  - Install pre-requisites:
    * [NodeJS](nodejs.org) and then follow [instructions for installing Particle CLI](https://docs.particle.io/guide/tools-and-features/cli/photon/#installing)
    * On Windows: you will need the [Particle USB Driver](https://s3.amazonaws.com/spark-website/Particle.zip)
    * [Connect your device over USB](https://docs.particle.io/guide/getting-started/connect/photon/#connecting-your-device-1)
    - Claim and configure WiFi on your device - optional but recommended
  - Edit your project (NOTEPAD is fine for that if you want)
  - Compile using Particle's online compiler
  - Upload the binary to your Photon over USB
  
# The Magic

Presuming you've already configured WiFi on your device, and you can see it in your https://dev.particle.io account the last remaining piece is now to do the coding!

The usual coding practice boils down to those steps:

  - Write code
  - Compile
  - Install/upload/flash newly compiled code/firmware
  - Debug and troubleshoot

## Source Code

As a start let's begin with the following simple program:

```C
void setup() {
    RGB.control(true);
}

void loop() {
   Serial.println("starting - LED off\r\n");
   RGB.color(0,0,0);
   delay(1000);
   
   Serial.println("starting - LED RED\r\n");
   RGB.color(255,0,0);
   delay(1000);
   
   Serial.println("starting - LED GREEN\r\n");
   RGB.color(0,255,0);
   delay(1000);
   
   Serial.println("starting - LED BLUE\r\n");
   RGB.color(0,0,255);
   delay(1000);
   
}
```

Save it as "led1.ino" (or anything else but keep the .ino extension) and create also a "particle.include" project file that lists the files from your project (just led1.ino so far) and save it also in the same folder:
```
led1.ino
```

## Compile

The easiest way to compile your program is to use Particle's online compiler via the [particle-cli](https://github.com/spark/particle-cli) command-line interface :

  particle compile photon . --saveTo fw.bin

which will:
  - compile for PHOTON API (or you can specify ELECTRON, or your device name and it will figure out what it is and use that API)
  - look for a project file in the current directory (it will look for the "particle.include" file there)
  - save the compiled firmware into "fw.bin" file
  
That's all!

## Upload newly compiled firmware

If you want you can push the new firmware via the USB cable, or you can tell Particle.io to remote-flash your device with the new firmware.

To upload it locally via USB here is an example of the command:

  particle flash --serial fw.bin

or if you want to flash your "MyPhotonDevice" trough the web:

  particle flash MyPhotonDevice fw.bin

## Debugging

Unfortunately there is no integrated debugging. So that part is not exactly easy.

A few relatively alternatives exist though:
  - Blink a LED! That's my personal favorite! :-) 
  - Use Serial.print to send debug data over the serial port
  - Stuff data into online variables, they'll be pushed to particle's servers and you can see them that way
  - Use a combination of those
  - If you must stop the program execution you can use for example a loop waiting for pressing of a button (but be careful with that)
  
# Conclusion

Even though not exactly the best (because of the missing debugger!) coding for Photon and Electron is very easy!

All of the standard Arduino libraries are supported too. 

## Some useful links:

  - [Particle's official Getting Started](https://docs.particle.io/guide/getting-started)
  - [Device functions and API](https://docs.particle.io/reference/firmware/core)
    - which closely mimic [Arduino Libraries Reference](https://www.arduino.cc/en/Reference/Libraries)
    - Language reference is pretty much C/C++ - here is [Arduino's Language Reference](https://www.arduino.cc/en/Reference/HomePage)
  - [Particle Devices Hardware Libraries](https://github.com/spark/hardware-libraries)
  - [Spark Firmware](https://github.com/spark/firmware) - in case you wanted to just see how low-level functions are implemented (let's say Wire library implements the [i2c](https://github.com/spark/firmware/blob/develop/hal/src/core/i2c_hal.c) functions)
  - [particle-cli command-line interface](https://github.com/spark/particle-cli) project on GitHub
  - Sparkfun guide: [Enginursday: Choose Your Photon IDE Adventure](https://www.sparkfun.com/news/1907)
  - Sparkfun's [Photon Development Guide - ARM GCC and the DFU Bootloader (Offline)](https://learn.sparkfun.com/tutorials/photon-development-guide/arm-gcc-and-the-dfu-bootloader-offline)
  - [Local development and gdb debugging with NetBeans, a step by step guide](https://community.particle.io/t/local-development-and-gdb-debugging-with-netbeans-a-step-by-step-guide/7829)
  - A very good example on how to set up your own custom library if you want to include it in the web/browser editor, it also shows how to use the SPI and I2C libraries: [Photon IMU Shield Hookup Guide](https://learn.sparkfun.com/tutorials/photon-imu-shield-hookup-guide)
  - Sparkfun's [Tutorials](https://learn.sparkfun.com/tutorials)
    - for example on how I2C works : https://learn.sparkfun.com/tutorials/i2c


## Final words

Hopefully you found this tutorial helpful! And I would certainly like to hear from you if you have any feedback, and if so please PM me on GitHub! 

Happy coding! :)
