---
layout: default
title: Wicked Rainman's projects
---

# Programming projects 
---------------------
__DAPL__     

Spent quite a while writing the _Data Analist Programming Language_. It's supposed to make life a bit easier when your looking for interesting patterns of activity in things like Web logs Etc. The whole idea seems to have fallen on deaf ears (maybe because it's no good), but I've left the code around just in case anyone shows any interest. Have a look [here](https://github.com/wicked-rainman/DAPL "Go on, click it. You know you want to!") if you are interested.   

------------

__Micro dot pHAT for a Raspberry Pi__

![](/pictures/phat1.png "It's upside down so the Raspberry pi can sit flat")

Recently bought a Micro Dot pHAT to go on a Raspberry Pi. Onboard are three smt IS31FL3730 chips and three pairs of matrix displays all driven over I2C.  It comes as a kit so you have to solder on the GPIO connector and all the DIL displays (The IS31FL3730 have already been installed). This took me about half an hour.  

I couldn't find  any C programs to get the board going (everyone seems to love python these days!) In the end I grabbed fragments of code I found on the Internet and wrote a small set of [functions](https://github.com/wicked-rainman/Rpi-Micro-Dot-pHAT "Print a string, update and reset the display and set brightness") that I think are useful. Help yourself if you were looking for a simple solution.

-------------------

__Indoor display for Aercus IP weather station__

A few years ago I purchased an [Aercus](http://www.aercusinstruments.com/aercus-instruments-weathersleuth-professional-ip-weather-station-with-direct-real-time-internet-monitoring/ "God bless the Aercus folks in New Zealand, but you can buy them in the UK from www.greenfrogscientific.co.uk" ) weather station. and configured it to send all the data to Weather Underground. My only complaint about this devices is it doesn't come with an indoor display.  

You can view the weather by directly connecting to the device's HTTP port, but I wanted something I could glance at without firing up a PC. To solve this I used a Raspberry Pi with a [Micro dot pHAT](https://shop.pimoroni.com/products/microdot-phat?variant=25454635591 "Go Sheffield!!!" ) attached and wrote a bit of [code](https://github.com/wicked-rainman/Aercus-IP-weather-station) that connects over WiFi and scrapes the web page. 

The code runs in a loop forever, so you either need to background it as a process or write a daemon so it runs from boot.  

----------------------------
