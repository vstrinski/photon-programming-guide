# Programming Photon's Particle - Beginner's Guide

First - congratulations for your choice on selecting [Particle](https://www.particle.io)'s Internet-Of-Things boards! Both the [Photon](https://www.particle.io/prototype#photon) (Wi-Fi) and [Electron](https://www.particle.io/prototype#electron) (GSM cellular) are a great option for beginners!

You can even call them the WiFi or Cellular equivalent of the [Arduino&copy;](www.arduino.cc)!

With very little development effort both boards allow you to build connected (to the Internet) devices and have them push data out and consume data in. Aside from the device API there is also cloud API which lets you consume and use that data and do many wonderful things.

TLDR? If you want you can skip the overview and go straight to the [The Guide](#the-guide) !

## Overview

In this guide we'll be focusing on the Photon device. Most of the instrictions apply to the Electron too.

You can find the official documentation at https://docs.particle.io/guide/getting-started/start/photon/ but in case you already have some coding experience you might find it somewhat lacking.

Most of Particle's documentation is written with Mac users in mind and if you happened to have a PC things may seem overly complicated.

Hence this guide and the goal to keep them simple!

### "The KISS Principle" or "Can I use NOTEPAD as my editor?"

Isn't it surprisign how oftern we get carried away in our desire to make it nice, and pretty, and full-featured, and it just ends up complicated? Let's Keep It Simple!

The Photon is awesome in providing simplicity for doing small projects! Developing for it can also be as simple! :)

The goals of this guide are to provide you with a very basic development environment, and where you can have your first program up and running in minutes. No complicated drivers installation. Very few (one!) prerequisites to install!  No special editors.

Yup! You read that right - you can use Notepad as your editor if you wish! 

It really is that simple! :-)

# Photon, development and IDE options

You may have searched the internet already and may have [found](https://www.sparkfun.com/news/1907) that there are essentially 3 choices when selecting your IDE and development environment. 

Here they are again in order from simplest to most comlicated:

  - All-online, where everything happens over the web
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
    * Use JTAG for hardware debuggin (ST-Link/ST-Link V2) with NetBeans or Eclipse

# The Guide

This guide presumes that you like using your favorite editor and want to have all of your source code stored locally on your computer.

## Keep It Simple!

For simplicity we'll stay away from USB cables and drivers. We'll use the cloud and web for as much as possible and just keep our favorite editor!

Here is an overview of the process:
  * Claim and initially configure your device (using phone, or see below for doing that using your computer and a USB cable)
  * Install "The Prerequisite" software - (Node.JS)[nodejs.org] with Particle's Command-Line Interface (CLI) which runs on top of NodeJS
  * Edit locally (yup, NOTEPAD is just fine!) - you can use one of the examples from this repository as a start
  * Use Particle's online compiler
  * Push updated firmware to your device via the web


## The slightly more reliable and yet still simple way

Unfortunately registering your device using just your tablet or cell phone isn't always as simple as it sounds. And what if your WiFi is somewhat picky, maybe too protected, add some networking/dhcp/firewall/etc issues in the mix, etc and suddenly getting those updates pushed to your Photon just don't work?

A USB cable is your solution!

Here is how the process looks in summary:

  - Install pre-requisites:
    * (NodeJS)[nodejs.org] and then follow [instructions for installing Particle CLI](https://docs.particle.io/guide/tools-and-features/cli/photon/#installing)
    * On Windows: you will need the [Particle USB Driver](https://s3.amazonaws.com/spark-website/Particle.zip) - if you need more details and instructions they're in the link below
    * [Connect your device over USB](https://docs.particle.io/guide/getting-started/connect/photon/)
  - Claim anc configure WiFi on your device - optional and probably not really necessary, but may make later steps a bit easier.
  - Compile your first program - you can use the examples from this repository
  - Upload the binary to your Photon over USB
  


