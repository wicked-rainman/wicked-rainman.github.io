---
layout: default
title: Wicked Rainman's projects
---

# Programming projects  

---------------------

__Indoor display for Aercus IP weather station__

A few years ago I purchased an [Aercus](http://www.aercusinstruments.com/aercus-instruments-weathersleuth-professional-ip-weather-station-with-direct-real-time-internet-monitoring/ "God bless the Aercus folks in New Zealand, but you can buy them in the UK from www.greenfrogscientific.co.uk" ) weather station. and configured it to send all the data to Weather Underground. My only complaint about this devices is it doesn't come with an indoor display.  

You can view the weather by directly connecting to the device's HTTP port, but I wanted something I could glance at without firing up a PC. To solve this I used a Raspberry Pi with a [Micro dot pHAT](https://shop.pimoroni.com/products/microdot-phat?variant=25454635591 "Go Sheffield!!!" ) attached and wrote a bit of [code](https://github.com/wicked-rainman/Aercus-IP-weather-station) that connects over WiFi and scrapes the web page. 

The code runs in a loop forever, so you either need to background it as a process or write a daemon so it runs from boot.  

----------------------------

__Micro dot pHAT for a Raspberry Pi__

![](/pictures/phat1.png "It's upside down so the Raspberry pi can sit flat. I've coded the fonts so they are up-side down too.")

Recently bought a Micro Dot pHAT to go on a Raspberry Pi. Onboard are three smt IS31FL3730 chips and three pairs of matrix displays all driven over I2C.  It comes as a kit so you have to solder on the GPIO connector and all the DIL displays (The IS31FL3730 have already been installed). This took me about half an hour.  

I couldn't find  any C programs to get the board going (everyone seems to love python these days!) In the end I grabbed fragments of code I found on the Internet and wrote a small set of [functions](https://github.com/wicked-rainman/Rpi-Micro-Dot-pHAT "Print a string, update and reset the display and set brightness using the chip's PWM and Current registers") that I think are useful. Help yourself if you were looking for a simple solution.

-------------------

__DAPL__     

Spent quite a while writing the _Data Analist Programming Language_. It's supposed to make life a bit easier when your looking for interesting patterns of activity in things like Web logs Etc. The whole idea seems to have fallen on deaf ears (maybe because it's no good), but I've left the code around just in case anyone shows any interest. Have a look [here](https://github.com/wicked-rainman/DAPL "Go on, click it. You know you want to!") if you are interested.   

------------

__War driving with an M5Stack__

![](/pictures/M5stack.png "You would have thought I could have cleaned the crud off the screen before taking the picture, but no!")

I sometimes view the [M5Stack](https://m5stack.com/ "You can buy them in the UK from several sources") as a neat substitute for an Arduino (I guess it all depends on what you plan to do). I was attracted to it because it's modular, comes in a cool case and has a built in display and buttons. 

I bougth the Fire version because it's red and has some additional built in sensors that the other versions don't have (Mostly, if I'm honest I bought it because its red). If you buy this version then you loose the use of some of the ESP32 IO pins, but you pays your money and takes your choice!

There's also a range of backpack styled modules available. They get attached to the back of the unit and are held in place by magnets embedded in the case. All in all, quite a fun product to play with. I shelled out further and bought a GPS backpack. WiFi and Bluetooth are built in, so that meant I could write some [war driving code and a bluetooth scanner](https://github.com/wicked-rainman/M5Stack-Fire "WiFi and Bluetooth scanning"). With the addition of a  usb battery bank, it seems to work very well!

--------------------------
